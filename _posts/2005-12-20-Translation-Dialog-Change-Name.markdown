---
layout: blogs_item
title: 【翻译】对话：换个名字
author: AcePeak
categories:
  - 积累
tags:
  - C++
  - OOP
  - Design Pattern
  - 原创
---

> 系列列表：
>
> [【翻译】对话：究竟谁才是可移植的程序员？]({% post_url 2005-11-19-Translation-Dialog-Portable-Design %})
>
> [【翻译】对话：接触指针]({% post_url 2005-11-28-Translation-Dialog-Touching-Pointers %})
>
> [【翻译】对话：换个名字]({% post_url 2005-12-20-Translation-Dialog-Change-Name %})

仅仅挂起100公里的距离，小行星就迅速占满了我们的视线。它的表面看起来就像碎过又用冰粘起来的杯子。很多的冰河在交错的小山脊间静静的流淌。木卫二，荒凉而美丽的地方。

这时喇叭响起，“请大家登机，三号舱和七号舱。”然后又安静下来了。

Jeannine和我在一小群专家团同事们中挤到窗口附近，大概我们很多人正在像发呆的学生们一样看着整个世界。我们不在乎。当然在飞船里面的任何屏幕都可以更好的观察，但这里有些很特殊很原始的光线，那是从月亮直接反射到我们的眼睛里面的光线。

“一个可以观察的很好的地方，”Jeannine跃跃欲试，“他们仍然对谣言很谨慎。”

“还没开始‘谨慎’。Ganymede这么说，Ganymede又那么说。他们本已告诉我们真正的目的了。”

“是的。我确定我们不久会在冰层下面找出他们发现的东西。”

“嗯？恩。”我反应了一下。“我很高兴能成为这里的参观者。我从前就已经看到了这漂亮虚幻的一幕，这很好了已经，不，更好了。我们真的在这里了。这让我想起了我的第一个工作。”

她调皮的喷了口鼻息。“每件事情都会让你想起你的第一份工作。”

“所以我才年轻又敏感。总之，现在参观到这里的一番谈话又让我想起了它。”

“阿。”顿了顿，吊吊胃口，然后：“你的意思是？”

我笑了，继续讲述。。。


-----------------------------------------------------------------------

我一直在与一个设计问题作斗争。我很想独立解决，因为我的试用期快结束了并且我想证明我自己。你也还记得你试用期之后的第一份工作，是吧？把事情做好是多么重要的事情？我亲眼看到其他的新员工没有通过试用期因为他们对付不了Guru。别误会，它是很出色的程序员，只不过有点古怪。现在她是我的老师，不为别的，就是因为我想向她证明我自己的能力。

我在一个类体系里需要一个新的虚函数，但是另一个组在维护它并且不会让别人改动它的。它看起来是这样的：


{% highlight C++ %}
class Personnel
{
public:
 virtual void Pay (/**/ ) = 0;
 virtual void Promote( /**/ ) = 0;
 virtual void Accept ( PersonnelV& ) = 0;
 // other functions
}

class Officer : public Personnel { /* override virtuals */ };
class Captain : public Officer { /* override virtuals */ };
class First : public Officer { /* override virtuals */ };
{% endhighlight %}


我需要一个函数，如果对象是船长，做一件事；如果是大副，就做另一件事。一个在Personnel或Officer声明在Captain和First里覆盖的虚函数本可以完成完成这件事的。

问题在于我不能增加一个函数。我知道我也能通过简单的增加使用RTTI的类型检测来完成工作，比如：


{% highlight C++ %}
void f( Officer &o)
{
 if( dynamic_cast<Captain*> (&o) )
 /* do one thing */
 else if( dynamic_cast<First*> (&o) )
 /* do another thing */
}

int main()
{
 Captain k;
 First s;
 f( k );
 f( s );
}
{% endhighlight %}


但是我知道在公司的代码标准里这样的类型检测是不允许的。“我不喜欢它，”我对自己说，“但是我想我这次必须要改变对它的看法了。显然没有其他方法了。”

“任何问题都可以通过增加一个中间层的方法来解决。”

我被身后Guru的声音吓了一跳。“什么？”我问道，转向了她。

“任何问。。。”

“是的，”我打断了她，忘了自己是谁了。“我听到你说的了，我只是不知道你从哪里来的。”我想这是我的掩饰。没人敢打断她的谈话。

“阿，但你知道的。”Guru斜着眼看着我，“你知道的，我的小学徒。”她注视了我一会，然后提高声音说，“孩子，C语言的弟子们会常用switch判断来控制对象类型的程序流。看看这个。”她拿起了一支涂写笔：


{% highlight C++ %}
/* A not-atypical C program */
void f(struct someStruct *s)
{
 switch(s->type) {
 case APPLE:
  /* do one thing */
  break;
 case ORANGE:
  /* do another thing */
 /*  etc.  */
 }
}
{% endhighlight %}


“当那些弟子们学习先知Stroustrup时，”她继续说，“在学习C++方面，他们必须学习如何设计好的类体系结构。”

“是的，”我又一次打断了她，急于显示我确实知道。“他们应该建立一个类结构体系来把Fruit作为积累，派生出Apple类和Orange类。那么‘do something’的代码会成为派生类的虚函数。”

“很好，孩子。C++的弟子们常常会用我刚刚讲的比喻来劝C的弟子们改变作风，他们指出switch状态检测是一种有错误倾向的需要常常维护的事情。但是，看看这个比喻的另一种方法：通过引入了一个虚函数，你增加了一个中间层。”她放下笔，“你需要的不就是一个新的虚函数吗？”
“阿，对。我知道，”我马上神气起来。“但我不能在这里那样做。”

她点了点头。“因为你不能修改类结构，对吧。”

这又使我恢复了平静，不过只是一瞬间。“哦，你知道了？我们不能改动它？原来你知道阿。”

“哦，是的。是我设计的这个结构。”

“哦。”这完全浇灭了我。

“这个结构必须非常稳定，因为有不多见的跨平台的依赖性。但是这样设计出来是让你增加虚函数来避免switch类型的代码的。你可以通过增加一个中间层来解决你的问题。在想象那个比喻。知道Personnel::Accept是什么吗？”

“唔，恩？”我含糊了声。

“这个类实现了一个未命名的模式（PNP）。也就是Visitor模式。”

“唔！”我说，现在有点明白了。“我已经看过Visitor了。但是那只是为允许对象之间可以迭代访问的机制。不是吗？”

她叹了口气，“这是流行的误解。想想那个V的意思，与其叫Visitor，不如叫Virtual，”她解释说。“这个PNP的最有用的应用就是允许增加虚函数到一个已存在的类结构里面，而不用改变现有的类结构。记得开始Personnel里面实现的那个Accept和它的子类吗？”她在下面的代码停了下来：


{% highlight C++ %}
void Personnel::Accept( PersonnelV& v )
{
 v.Visit( *this );
}
void Officer::Accept ( PersonnelV& v )
{
 v.Visit( *this );
}
void Captain::Accept ( PersonnelV& v )
{
 v.Visit( *this );
}
void First::Accept ( PersonnelV& v )
{
 v.Visit( *this );
}
{% endhighlight %}


“而且，”她继续说道，“Visitor的基类是这样的：”


{% highlight C++ %}
class PersonnelV /*Visitor*/
{
public:
 virtual void Visit( Personnel& ) = 0;
 virtual void Visit( Officer& ) = 0;
 virtual void Visit( Captain& ) = 0;
 virtual void Visit( First& ) = 0;
}
{% endhighlight %}


“阿，”我说，我想起来了。“那么当我写了使用派生自Personnel的对象的代码时，我只要调用Personnel::Accept( myVisitorObject )，因为Accept是一个虚的myVisitorObject。Visit会被正确的继承类型来调用，重载机制会选择正确的函数。那就相当于增加了一个新的虚函数了，是吗？”

“确实，孩子。新增加的函数一般要用客户类的公有接口，但是怀着尊敬，它能并且在表现的像个虚函数而并不通过成员。我们所需要的就是原有的体系支持的借口Accept，就像是开放自己用于扩展。如果以后我们发现我们常常要通过新的子类来扩展访问到的Personnel体系，或者我们想更好的管理重新编译的依赖性，我们可以移植到非循环的Visitor（Acyclic Visitor）--在它们Accept函数重新声明前就不再需要改动Personnel和它的子类。”

我知道了。“ok，那么我可以这样做：”我快速的写下了：


{% highlight C++ %}
class DoSomething : public PersonnelV
{
public:
 virtual void Visit ( Personnel& );
 virtual void Visit ( Officer& );
 virtual void Visit ( Captain& );
 virtual void Visit ( First& );
}

void DoSomething::Visit( Captain& c )
{
  if( femaleGuestStarIsPresent )
    c.TurnOnCharm();
  else
    c.StartFight();
}

void DoSomething::Visit( First& f )
{
  f.RaiseEyebrowAtCaptainsBehavior();
}
{% endhighlight %}


Guru对我的代码很满意了。“你刚才说这样的代码是为什么系统工作的呢？”

“阿...一个模拟器？”

“我知道。继续，孩子，写出剩下的代码。”我又增加了下面的代码：


{% highlight C++ %}
void f( Personnel& p )
{
  p.Accept( DoSomething() ); // like p.DoSomething()
}

int main()
{
  Captain k;
  First s;

  f( k );
  f( s );
}
{% endhighlight %}


Guru走回去了，又把她那独特的声音塞入我的耳朵。“确实，这个函数并不通过Personnel::域名字直接继承自原来的体系了。在这个例子里，换了另一个名字的函数仍然是虚的。”他笑了笑，悄悄地走了。她的话又飘了出来直到她走出我的视线：“Visitor模式换个名字会仍然有用，甚至会更合适的描述。但是世事难料啊。。。”

----------------------------------------------

宏伟的木星显得很庄严，甚至淡化了木卫二表面的美丽，当飞船旋转的时候，木星开始进入屏幕视角。

“我会申请一些表面合适的时间，”我决定。“多么适合散步的天空阿。甚至我只是一个参观者。”

“我们都是参观者，”Jeannine同意道。“但是我觉得，我们是第一个吗？”

随后片刻，我们都只是静静地观看。
