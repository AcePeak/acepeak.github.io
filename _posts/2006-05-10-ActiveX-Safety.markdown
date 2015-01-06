---
layout: news_item
title: 剖析ActiveX控件安全问题
author: AcePeak
categories: [Internet]
tags: 
- 原生
- C++
- ActiveX
- Safety
---


##1、介绍

如果你曾经在网页或者ASP中使用过com对象，你可能会发现，有时候会出现这样讨厌的对话框

![对话框](/img/060510_1.jpg)

这是因为你的控件没有被标记为安全的，对于初始化不安全或者对于脚本不安全，甚至兼而有之。你每打开一次这样的网页，这种情况就会发生一次，你怎么办？当然，这可以通过设置IE本身的安全等级为low来解决这样的问题，但是如果你要制作一个可发布的控件，你能想象到每一位用户在使用你制作的控件时都要且列抱怨这种强制行为；或者如果你是其中一个使用者，当你同样遇到这种情况之后不得不将自己的IE安全等级设置为low，与此同时你平时上网过程中那些行为不轨的控件有时也会悄然而至，你的灾难来了！作为一个聪明的程序员，你不能要求任何用户做一些不切实际或者不够安全的改变来适应你的产品，因为你知道那只会使你的控件被逐渐打入冷宫，到最后销声匿迹，那不是你想要的。我们要消灭掉这样的对话框而且还不让用户发现丝毫安全上和使用上的失望。本文就是横向探讨在C++编程环境下如何消除这些问题的。


##2、原理

ActiveX控件是一种极其危险的提供功能的方法（目前正在被MS逐渐冷落），因为它是一种组建对象模型（COM）的对象，只要电脑的用户可以完成的任务，它都可以完成。比如它可以存取注册表，可以随意访问本地文件系统等等。一个网页上面的控件一般有2种不安全的状态，一种是脚本的不安全，一种是初始化的不安全。当用户将一个压缩解压缩控件指向一个远程被压缩的包含特洛伊木马的系统文件并且需要控件来解压缩这个文件时，系统安全会被打破。这个状态就是初始化的不安全。从代码的角度来讲，如果控件从IPersist派生，也就是说控件实现了永久性，那么就会触发unsafe for initializing。而在脚本程序安全执行以前，一个控件依赖于特定的系统设置，那么在允许这段代码运行之前，控件的开发人员需要提供一些必要的代码。从代码的角度来讲，如果控件从IDispatch派生，也就是说控件支持脚本，那么就会触发unsafe for scripting。

从用户下载一个ActiveX控件开始，这个控件甚至可能很容易被攻击，因为网络上任何网络程序都可以使用它，无论是出于友好的目的还是恶意的目的。因此IE浏览器（本文只探讨IE内核的浏览器）总是试图弹出一个对话框来告诉你，这个控件可能是不安全的。这几乎总是一个很好的预防网络攻击的好方法，但是对于那些我们认为总是安全的控件，我们仍然要总是接受这种IE产生的干扰，这就使人厌烦了。其实当身为程序员的你写这样的安全控件时，这样的问题是很容易解决的。 


##3、解决方法

目前，对这个问题的解决方法主要有几种：使用数字签名，继承IObjectSafety接口，修改注册表等。


###3.1、使用数字签名
数字签名是一种使控件足够安全的方法，它通过特定的密钥来加密控件的使用，使得使用控件的对象能够根据密钥是否相符来检测控件是否足够安全。通常，拥有自己的可发布的数字签名是要Money的，本文是一篇技术文章，对此并不深入探讨，下面主要介绍代码方面的安全化。

###3.2、继承IObjectSafety接口
IObjectSafety接口是在头文件"objsafe.h"中定义的接口，定义如下： 

{% highlight C++ %}
IObjectSafety : public IUnknown
{
    public:
    virtual HRESULT STDMETHODCALLTYPE GetInterfaceSafetyOptions( 
    /* [in] */ REFIID riid,
    /* [out] */ DWORD *pdwSupportedOptions,
    /* [out] */ DWORD *pdwEnabledOptions) = 0;

    virtual HRESULT STDMETHODCALLTYPE SetInterfaceSafetyOptions( 
    /* [in] */ REFIID riid,
    /* [in] */ DWORD dwOptionSetMask,
    /* [in] */ DWORD dwEnabledOptions) = 0;
};
{% endhighlight %}

其中参数意义如下：

{% highlight C++ %}
//riid                Interface identifier for the object to be made safe. 
//
//dwOptionSetMask     Options to be changed. 
//
//dwEnabledOptions    Settings for the options that are to be changed. This can be one of the following values. 
//                    INTERFACESAFE_FOR_UNTRUSTED_CALLER
//                        Indicates the interface identified by riid should be made safe for scripting. 
//                    INTERFACESAFE_FOR_UNTRUSTED_DATA
//                        Indicates the interface identified by riid should be made safe for untrusted data during initialization.
{% endhighlight %}


这个接口允许容器询问控件是否安全或者改变控件的安全属性。目前IObjectSafety支持四种安全属性，但是一般我们只使用前两个：脚本安全和初始化安全。这些属性定义如下：

{% highlight C++ %}
// Option bit definitions for IObjectSafety:
#define    INTERFACESAFE_FOR_UNTRUSTED_CALLER        0x00000001    // Caller of interface may be untrusted
#define    INTERFACESAFE_FOR_UNTRUSTED_DATA          0x00000002    // Data passed into interface may be untrusted
#define    INTERFACE_USES_DISPEX                     0x00000004    // Object knows to use IDispatchEx
#define    INTERFACE_USES_SECURITY_MANAGER           0x00000008    // Object knows to use IInternetHostSecurityManager
{% endhighlight %}


####3.2.1、实现方法

首先包含头文件

{% highlight C++ %}
#include "objsafe.h"
{% endhighlight %}


然后是自己的控件类继承IObjectSafetyImpl

{% highlight C++ %}
class YourClass :
    public IObjectSafetyImpl<YourClass, INTERFACESAFE_FOR_UNTRUSTED_CALLER | INTERFACESAFE_FOR_UNTRUSTED_DATA>
{
{% endhighlight %}


其中`INTERFACESAFE_FOR_UNTRUSTED_CALLER | INTERFACESAFE_FOR_UNTRUSTED_DATA`代表默认这个控件是脚本安全而且初始化安全的。然后在com接口表中添加接口名

{% highlight C++ %}
BEGIN_COM_MAP(CCGrid)
    
    COM_INTERFACE_ENTRY(IObjectSafety)
END_COM_MAP()
{% endhighlight %}


OK，大功告成。这也是一种很简单的方法。

###3.3、修改注册表

修改注册表项使控件支持安全类别的原理，归根到底其实就是下面的第三个方法，另外两个方法都是对这个方法的外围包装和更加安全的处理。修改注册表在不同的工程中有着不同的表现：

####3.3.1、用于ATL属性工程的com接口

因为VC的属性工程已经加入了安全控件的注册表支持，并且直接加入了关键字implements_category，因此我们仅仅象下面这样既可完成安全属性设置：

{% highlight C++ %}
[
    coclass/progid/vi_prgid,            //必须至少有其中一个
    
    implements_category("CATID_SafeForScripting"),
    implements_category("CATID_SafeForInitializing"),
    
]
{% endhighlight %}


不过要注意的是，对于类似下面的代码（往往是非属性工程的）是不能添加的：

{% highlight C++ %}
[
    uuid(),
    helpstring("")
]
coclass YourCtrl
{
    [default] interface ,
        [default,source] dispinterface 
}
{% endhighlight %}


因为这种coclass是IDL的属性，而IDL本身并没有安全功能。

而上面的那种coclass是VC的属性，MS提供了对安全控件的支持。

####3.3.2、主要用于非属性工程的通用方法

在类声明文件中加入头文件

{% highlight C++ %}
#include "objsafe.h"
{% endhighlight %}


在类声明中添加如下代码：

{% highlight C++ %}
   BEGIN_CATEGORY_MAP( YourCtrlClassName )
       IMPLEMENTED_CATEGORY( CATID_SafeForScripting )
       IMPLEMENTED_CATEGORY( CATID_SafeForInitializing )
   END_CATEGORY_MAP()
{% endhighlight %}


即可使其支持safety属性，当然你也可以选择性的只支持一种安全属性。

####3.3.3、主要用于MFC ActiveX Control的通用方法

在$project.cpp文件中添加以下代码：

{% highlight C++ %}
#include "comcat.h"
#include "Objsafe.h"

// 控件的CLSID,注册表用（一定要是实际使用的控件的）
const GUID CDECL CLSID_SafeItem ={ 0x7AE7497B, 0xCAD8, 0x4E66, { 0xA5,0x8B,0xDD,0xE9,0xBC,0xAF,0x6B,0x61 } };

// 版本控制
const WORD _wVerMajor = 1;

// 次版本号
const WORD _wVerMinor = 0;

//////////////////////////////////////////////////////////////////////
// 创建组件种类
HRESULT CreateComponentCategory(CATID catid, WCHAR* catDescription)
{
    ICatRegister* pcr = NULL ;
    HRESULT hr = S_OK ;

    hr = CoCreateInstance(CLSID_StdComponentCategoriesMgr, NULL, CLSCTX_INPROC_SERVER, IID_ICatRegister, (void**)&pcr);
    if (FAILED(hr))
        return hr;

    // Make sure the HKCR\Component Categories\{..catid}
    // key is registered.
    CATEGORYINFO catinfo;
    catinfo.catid = catid;
    catinfo.lcid = 0x0409 ; // english

    // Make sure the provided description is not too long.
    // Only copy the first 127 characters if it is.
    int len = wcslen(catDescription);
    if (len>127)
        len = 127;
    wcsncpy(catinfo.szDescription, catDescription, len);

    // Make sure the description is null terminated.
    catinfo.szDescription[len] = '\0';

    hr = pcr->RegisterCategories(1, &catinfo);
    pcr->Release();

    return hr;
}

// 注册组件种类
HRESULT RegisterCLSIDInCategory(REFCLSID clsid, CATID catid)
{

    // Register your component categories information.
    ICatRegister* pcr = NULL ;
    HRESULT hr = S_OK ;
    hr = CoCreateInstance(CLSID_StdComponentCategoriesMgr, NULL, CLSCTX_INPROC_SERVER, IID_ICatRegister, (void**)&pcr);
    if (SUCCEEDED(hr))
    {

        // Register this category as being implemented by the class.
        CATID rgcatid[1] ;
        rgcatid[0] = catid;
        hr = pcr->RegisterClassImplCategories(clsid, 1, rgcatid);
    }
    if (pcr != NULL)
        pcr->Release();
    return hr;
}

// 卸载组件种类
HRESULT UnRegisterCLSIDInCategory(REFCLSID clsid, CATID catid)
{
    ICatRegister* pcr = NULL ;
    HRESULT hr = S_OK ;

    hr = CoCreateInstance(CLSID_StdComponentCategoriesMgr, NULL, CLSCTX_INPROC_SERVER, IID_ICatRegister, (void**)&pcr);
    if (SUCCEEDED(hr))
    {

        // Unregister this category as being implemented by the class.
        CATID rgcatid[1] ;
        rgcatid[0] = catid;
        hr = pcr->UnRegisterClassImplCategories(clsid, 1, rgcatid);
    }

    if (pcr != NULL)
        pcr->Release();

    return hr;
}
{% endhighlight %}

修改以下函数：

{% highlight C++ %}
// DllRegisterServer - Adds entries to the system registry
STDAPI DllRegisterServer(void)
{
    HRESULT hr;

    AFX_MANAGE_STATE(_afxModuleAddrThis);

    if (!AfxOleRegisterTypeLib(AfxGetInstanceHandle(), _tlid))
        return ResultFromScode(SELFREG_E_TYPELIB);

    if (!COleObjectFactoryEx::UpdateRegistryAll(TRUE))
        return ResultFromScode(SELFREG_E_CLASS);

    // 标记控件初始化安全.
    // 创建初始化安全组件种类
    hr = CreateComponentCategory(CATID_SafeForInitializing, L"Controls safely initializable from persistent data!");
    if (FAILED(hr))
        return hr;

    // 注册初始化安全
    hr = RegisterCLSIDInCategory(CLSID_SafeItem, CATID_SafeForInitializing);
    if (FAILED(hr))
        return hr;

    // 标记控件脚本安全
    // 创建脚本安全组件种类 
    hr = CreateComponentCategory(CATID_SafeForScripting, L"Controls safely scriptable!");
    if (FAILED(hr))
        return hr;

    // 注册脚本安全组件种类
    hr = RegisterCLSIDInCategory(CLSID_SafeItem, CATID_SafeForScripting);
    if (FAILED(hr))
        return hr;

    return NOERROR;
}

//////////////////////////////////////////////////////////////////
// DllUnregisterServer - Removes entries from the system registry
STDAPI DllUnregisterServer(void)
{
    HRESULT hr;
    AFX_MANAGE_STATE(_afxModuleAddrThis);

    if (!AfxOleUnregisterTypeLib(_tlid, _wVerMajor, _wVerMinor))
        return ResultFromScode(SELFREG_E_TYPELIB);

    if (!COleObjectFactoryEx::UpdateRegistryAll(FALSE))
        return ResultFromScode(SELFREG_E_CLASS);

    // 删除控件初始化安全入口.
    hr=UnRegisterCLSIDInCategory(CLSID_SafeItem, CATID_SafeForInitializing);
    if (FAILED(hr))
        return hr;

    // 删除控件脚本安全入口
    hr=UnRegisterCLSIDInCategory(CLSID_SafeItem, CATID_SafeForScripting);
    if (FAILED(hr))
        return hr;

    //////////////////////////
    return NOERROR;
} 
{% endhighlight %}


至此对工程的修改完成了，现在控件就可以在自注册时就注册为安全控件了！

####3.3.4、手动修改注册表

我们可以自己手动为控件在注册表中添加安全支持，实际上我们所需要的两个项（Key）就是这样的形式：

{% highlight C++ %}
\HKEY_LOCAL_MACHINE\SOFTWARE\Classes\CLSID\<GUID of control class>\Implemented Categories\<GUID of category>
{% endhighlight %}


ActiveX SDK头文件ObjSafe.H 已经为类别CATID_SafeForInitializing和CATID_SafeForScripting定义了GUID值。因此对于特定的工程，如果控件类的GUID是{20048BB3-DB68-11CF-9CAF-00AA006CB425}，那么我们就只需要添加两个注册表项：  

{% highlight C++ %}
   REGEDIT4
       
   [HKEY_CLASSES_ROOT\CLSID\{20048BB3-DB68-11CF-9CAF-00AA006CB425}\Implemented Categories]
       
   [HKEY_CLASSES_ROOT\CLSID\{20048BB3-DB68-11CF-9CAF-00AA006CB425}\Implemented Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]
       
   [HKEY_CLASSES_ROOT\CLSID\{20048BB3-DB68-11CF-9CAF-00AA006CB425}\Implemented Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]
{% endhighlight %}


将以上代码拷贝到一个*.reg中去，保存后执行就可以将GUID为{20048BB3-DB68-11CF-9CAF-00AA006CB425}的控件类注册为安全控件。有时候注册表中不一定有那两个类别，因此我们还需要自己来描述这两个重要的类别： 

{% highlight C++ %}
REGEDIT4

[HKEY_CLASSES_ROOT\Component Categories]

[HKEY_CLASSES_ROOT\Component Categories\{7DD95801-9882-11CF-9FA9-00AA006C42C4}]
"409"="Controls that are safely scriptable"

[HKEY_CLASSES_ROOT\Component Categories\{7DD95802-9882-11CF-9FA9-00AA006C42C4}]
"409"="Controls safely initializable from persistent data"
{% endhighlight %}


同样，将以上代码拷贝到*.reg文件中执行后，就可以生成这两个类别。以后就可以使用这两个类别来注册安全控件了。注意：除非你没有别的办法，千万不要使用这个方法，也不要使用这个方法来标记实际上并不安全的控件为安全控件。

那么方法3和方法1和2有什么不同的呢？其实他们最大的不同就是方法1和2实际上都加入各种判断代码在修改注册表之前和之后，实际上也防止了不安全控件注册为安全控件的行为。因此除非万不得已，不要用方法3。就算是方法1和方法2，也要在确定自己控件足够安全的情况下才使用。

###3.4、另一个问题

在施行了这些方法后，那个讨厌的对话框没了，但是对于window XP SP2及以上版本来说，用默认安全级别的IE打开任何包括了控件或者脚本的网页时，在运行代码前都会弹出一个这样的条框:

![对话框](/img/060510_2.jpg)

![对话框](/img/060510_3.jpg)

![对话框](/img/060510_4.jpg)


这也是为了不断提醒用户这样的操作可能会有安全上的危险，可是这样也会影响用户的操作，对于一个频繁访问的某一个页面来说，这个横条和对话框都是不易忍受的，如果你正在编写这样包括脚本和控件的页面，那么这里有一个窍门来解决这样的问题。请把下面这句加在网页文件源代码的<html>和<head>之间：

{% highlight C++ %}
<!-- saved from url=(0017)http://localhost/ -->
{% endhighlight %}

在你做网页时，如果网页需要运行ActiveX或脚本，并且他们位于客户端以外的地方，那么可以添加这个注释语句，IE当然不会不理他， IE会按照他指出的URL去找脚本的位置。 这句话的作用是让Internet Explorer 使用 Internet 区域的安全设置，而不是本地计算机区域的设置。其中0017代表后面网址的字符个数，后面的网址字符串要指向注册了这个组件或脚本的地方。如果是象上面那样，就表明是在自己的电脑上。把这句话删除，有些脚本就不执行了。

###3.5、什么是足够安全的控件

我怎么知道我的控件是不是足够安全呢？请好好看看这一节。一旦标注出现在控件上而非网页上时，那些标注为安全的控件就一定要在所有可能的网页上是安全的。因此一个控件被标注为安全的就表示它能够保护自己并与网页制作者可能在初始化或脚本过程中做的不愉快的东西隔离。实际上很容易检验当被用于网页时一个控件是否安全的：当你标注你的控件为初始化安全时，相当于你在发誓无论用什么样的值来初始化你的控件，都不可能发生伤害用户的系统或者威胁到用户的安全；当你标注你的控件为脚本安全时，那就是说你有把握说无论控件的函数和属性如何被网页的脚本操作，控件本身都不会做出危及用户安全的行为。换句话说，它必须接受任何脚本中任何顺序的函数和/或属性调用而不会发生危险。　在设计控件过程中，下面是一些表明此控件是安全的条款：

> * 不要操作用户的文件系统；
> * 不要操作注册表（除非是注册和注销它本身）；
> * 不要数组越界或其他的内存错误；
> * 验证（或更正）所有的输入，包括初始化，方法的参数和属性的Set函数；
> * 不要滥用与用户有关的活是用户提供的数据；
> * 做大量的测试。

这份表还远没有结束，但这些至少都是必要的。还有一点很重要，就是千万不要把本来实际上不安全的控件注册为安全的，尽管这很诱人（比如说你没有控件的源代码）。无论控件做什么事情的，一旦控件被标注为安全的，那么所有的网页都会省略对这个控件的安全检测。到目前为止，还没有方法能把一个控件标注为仅对特定网页是安全的。标注不安全控件为安全空间的一个简单安全的选择就是写一个包含了不安全控件的新安全控件。只要确保新安全控件的初始化，方法和属性都是安全的就行了。 

##4、总结

控件的安全问题可以通过各种各样的方法来巧妙的解决，但是对于一个负责的程序员来说，一定要确保控件本身是绝对安全的。一个欲发布的控件往往是要有用户使用的，如果本身不安全的控件被当成安全的控件流传出去，那就是恶意行为了。为了对用户负责，也为了对自己负责，程序员一定要再三检查自己的控件是否足够安全，而后再决定是否发布及以何种方式发布。