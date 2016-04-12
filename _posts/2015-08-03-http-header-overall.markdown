---
layout: blogs_item
title: HTTP请求头系列（1）-总览
author: AcePeak
categories:
  - 积累
tags:
  - 原创
  - HTTP
  - Header
---

> 系列列表：
>
> [HTTP请求头系列（1）-总览]({{site.url}}/blogs/2012/08/03/http-header-overall/)
>
> [HTTP请求头系列（2）-P3P]({{site.url}}/blogs/2012/08/04/http-header-P3P/)
>
> [HTTP请求头系列（3）-Cookies]({{site.url}}/blogs/2012/08/05/http-header-cookies/)


先来看一个现成的http请求头：

{% highlight bash %}
http://192.168.10.214/track?platform=1&type=1&item=hello&pos=1,2,3,4&url=www.baidu.com&aid=1111

General
	Remote Address:192.168.10.214:80
	Request URL:http://192.168.10.214/track?platform=1&type=1&item=hello&pos=1,2,3,4&url=www.baidu.com&aid=1111
	Request Method:GET
	Status Code:200 OK
Response Headers
	Cache-Control:private, no-cache, no-cache=Set-Cookie, proxy-revalidate
	Connection:keep-alive
	Content-Length:43
	Content-Type:image/gif
	Date:Tue, 11 Aug 2015 02:38:28 GMT
	P3p:CP=CURa ADMa DEVa PSAo PSDo OUR BUS UNI PUR INT DEM STA PRE COM NAV OTC NOI DSP COR
	Pragma:no-cache
	Server:nginx/1.8.0
	Set-Cookie:mmsid=0000000000000031;expires=Wed, 10 Aug 2016 02:38:28 GMT;domain=192.168.10.214;path=/
	X-Content-Type-Options:nosniff
	Last-Modified:Tue, 14 Jan 2014 07:16:10 GMT
Request Headers
	Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
	Accept-Encoding:gzip, deflate, sdch
	Accept-Language:en-US,en;q=0.8,zh-CN;q=0.6,zh;q=0.4,zh-TW;q=0.2
	Cache-Control:no-cache
	Connection:keep-alive
	Cookie:mmsid=0000000000000031
	Host:192.168.10.214
	Pragma:no-cache
	User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.134 Safari/537.36
	Referer:http://192.168.10.214/test
Query String Parameters
	platform:1
	type:1
	item:hello
	pos:1,2,3,4
	url:www.baidu.com
	aid:1111
{% endhighlight %}

针对不同的条目，进行一个简单的解释：

{% highlight bash %}
	Remote Address:192.168.10.214:80
{% endhighlight %}



{% highlight bash %}
	Request URL:http://192.168.10.214/track?platform=1&type=1&item=hello&pos=1,2,3,4&url=www.baidu.com&aid=1111
{% endhighlight %}

请求的url，当前请求的是一个API接口/track，后面跟了一些参数，实际上参数需要urlencode的，但是这里是手动请求所以没有。

{% highlight bash %}
	Request Method:GET
{% endhighlight %}

请求的方法，当前是GET。

这个字段是大小写敏感的，包括OPTIONS、GET、HEAD、POST、PUT、DELETE、 TRACE。

方法GET和HEAD应该被所有的通用WEB服务器支持，其他所有方法的实现是可选的。
webservice标准REST，一个请求就是请求一个资源，而用HTTP协议中自带的方法定义请求资源的状态（GET、POST、PUT、DELETE）。

{% highlight bash %}
	Status Code:200 OK
{% endhighlight %}

http状态码，表明这个请求响应的状态，是服务器返回来的，也就是8.su.bdimg.com返回的。

一个数字定义响应的类别，后两个数字没有分类的作用。第一个数字可能取5个不同的值：
1xx:信息响应类，表示接收到请求并且继续处理
2xx:处理成功响应类，表示动作被成功接收、理解和接受
3xx:重定向响应类，为了完成指定的动作，必须接受进一步处理
4xx:客户端错误，客户请求包含语法错误或者是不能正确执行
5xx:服务端错误，服务器不能正确执行一个正确的请求

{% highlight bash %}
	Cache-Control:private, no-cache, no-cache=Set-Cookie, proxy-revalidate
{% endhighlight %}

cache-control是用于控制网页的缓存，跟Expires同个意思。

max-age单位是秒，就是从现在开始到15552000之间都是有用的，这张图片都是被缓存下来的。
Cache-Control是HTTP1.1才有的，不适用与HTTP1.0，而Expires既适用于HTTP1.0，也适用于HTTP1.1。
Ctrl+F5时缓存无效，都会重新获取。

有以下几种取值：

max-age：（只接受 Age 值小于 max-age 值，并且没有过期的对象）
max-stale：（可以接受过去的对象，但是过期时间必须小于 max-stale 值）
min-fresh：（接受其新鲜生命期大于其当前 Age 跟 min-fresh 值之和的缓存对象）
响应：public(可以用 Cached 内容回应任何用户)
private（只能用缓存内容回应先前请求该内容的那个用户）
no-cache（可以缓存，但是只有在跟WEB服务器验证了其有效后，才能返回给客户端）

{% highlight bash %}
	Connection:keep-alive
{% endhighlight %}

客户端与服务器连接的类型。keep-alive和close两种，可以理解为长连接和短连接。其实是对应tcp的长连接和短连接。

HTTP是一个无状态的面向连接的协议。是在tcp上的应用层协议。
在HTTP/1.0中默认是close，短连接。就是每次请求完毕都立即关闭连接。
从 HTTP/1.1起，默认使用keep-alive，长连接。就是每次请求完毕仍然保持一段时间连接。

{% highlight bash %}
	Content-Length:43
{% endhighlight %}

服务器告诉浏览器自己响应的对象的长度。不包含http头的大小。这里就是指图片的大小，7183.png就是322B大小。

{% highlight bash %}
	Content-Type:image/gif
{% endhighlight %}

服务器返回的数据的mineType，是符合Accept要求的。一张png图片，是官方定义的资源类型。

{% highlight bash %}
	Date:Tue, 11 Aug 2015 02:38:28 GMT
{% endhighlight %}

信息发送的时间，GMT格林威治时间。

{% highlight bash %}
	P3p:CP=CURa ADMa DEVa PSAo PSDo OUR BUS UNI PUR INT DEM STA PRE COM NAV OTC NOI DSP COR
{% endhighlight %}

P3P 是 The Platform for Privacy Preferences 的简称，P3P header允许跨域访问隐私数据，从而可以跨域set-cookie成功。值得注意的是，P3P header只需要设置一次，这样跟在这个P3P header后面的所有 set-cookie，都可以跨域访问了。也就是说: 被P3P header设置过一次后，之后的请求不再需要P3P header，也能够在iframe里跨域发送这些cookie。但是如果用 set-cookie 去改变设置好的cookie，则不再具有这种跨域访问特性。P3P header 还有一个特点就是同一个包里只能设置一次，后面的P3P Header不会覆盖前面的P3P header，浏览器只认第一个。

可参考[HTTP请求头系列（2）-P3P]({{site.url}}/blogs/2012/08/04/http-header-P3P/)

{% highlight bash %}
	Pragma:no-cache
{% endhighlight %}

Pragma头域用来包含实现特定的指令，最常用的是Pragma:no-cache。在HTTP/1.1协议中，它的含义和Cache-Control:no-cache相同。

{% highlight bash %}
	Server:nginx/1.8.0
{% endhighlight %}

服务器的类型和版本

{% highlight bash %}
	Set-Cookie:mmsid=0000000000000031;expires=Wed, 10 Aug 2016 02:38:28 GMT;domain=192.168.10.214;path=/
{% endhighlight %}

Set-Cookie由服务器发送，它包含在响应请求的头部中。它用于在客户端创建一个Cookie。mmsid设置了一个自定义的键值对，expires定义了cookie的过期时间，domain定义了cookie生效的域名，path定义了cookie生效的路径。

请参考[HTTP请求头系列（3）-Cookies]({{site.url}}/blogs/2012/08/05/http-header-cookies/)

{% highlight bash %}
	X-Content-Type-Options:nosniff
{% endhighlight %}

这个header主要用来防止在IE9、chrome和safari中的MIME类型混淆攻击。firefox目前对此还存在争议。通常浏览器可以通过嗅探内容本身的方法来决定它是什么类型，而不是看响应中的content-type值。通过设置 X-Content-Type-Options：如果content-type和期望的类型匹配，则不需要嗅探，只能从外部加载确定类型的资源。

{% highlight bash %}
	Last-Modified:Tue, 14 Jan 2014 07:16:10 GMT
{% endhighlight %}

在浏览器第一次请求某一个URL时，服务器端的返回状态会是200，内容是请求的资源，同时将Last-Modified属性标记此文件在服务期端最后被修改的时间。
客户端第二次请求此URL时，根据 HTTP 协议的规定，浏览器会向服务器传送 If-Modified-Since 报头，询问该时间之后文件是否有被修改过：

Tue, 14 Jan 2014 07:16:10 GMT

如果服务器端的资源没有变化，则自动返回 HTTP 304 （Not Changed.）状态码，内容为空，这样就节省了传输数据量。当服务器端代码发生改变或者重启服务器时，则重新发出资源，返回和第一次请求时类似。从而保证不向客户端重复发出资源，也保证当服务器有变化时，客户端能够得到最新的资源。

{% highlight bash %}
	Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
{% endhighlight %}

告诉服务器自己接受什么介质类型（mineType），*/* 表示任何类型，type/* 表示该类型下的所有子类型，type/sub-type。

image/webp是指一种webp的图片格式，是google弄出来的。这种mineType不是官方定义的。

在质量相同的情况下，WebP格式图像的体积要比JPEG格式图像小40%。美中不足的是，WebP格式图像的编码时间“比JPEG格式图像长8倍”。

q是权重，*/*的权重是0.8，而image/webp的权重是默认值1.（q为0时，不接受这种类型）

这个句子的意思是我这个浏览器优先接受webp格式的图片，但是如果没有这种图片，那给我随便什么东西。

{% highlight bash %}
	Accept-Encoding:gzip, deflate, sdch
{% endhighlight %}

浏览器可以解码的编码方法（压缩方法）

gzip是 GNU zip 的缩写，它是一个 GNU 自由软件的文件压缩程序，也经常用来表示 gzip 这种文件格式。
deflate是同时使用了 LZ77 算法与哈夫曼编码（Huffman Coding）的一个无损数据压缩算法。
sdch是Chrome自己定义的压缩方法。
这些编码方法，都是为了减少传输的数据，需要服务器的支持。

假设8.su.bdimg.com服务器是nginx，可以开启gzip压缩功能，那么当我们的Chrome发送这个请求时，服务器会先将png用gzip算法压缩，再发到Chrome。然后Chrome解压缩，显示出来。

{% highlight bash %}
	Accept-Language:en-US,en;q=0.8,zh-CN;q=0.6,zh;q=0.4,zh-TW;q=0.2
{% endhighlight %}

浏览器支持的语言，中文简体和中文。优先支持中文。（上面解释过了q是权重的意思，zh-CN权重是1，zh权重是0.8）。

{% highlight bash %}
	Cookie:mmsid=0000000000000031
{% endhighlight %}

请求串将存在于当前域和当前路径的cookie发送给服务器。

{% highlight bash %}
	Host:192.168.10.214
{% endhighlight %}

主机是192.168.10.214，这个可以从request url里面看出来。

{% highlight bash %}
	User-Agent:Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/43.0.2357.134 Safari/537.36
{% endhighlight %}

最复杂的一个字段。user-Agent每个浏览器都不同，但都类似。

Mozilla/5.0基本上所有的浏览器都以Mozilla开头，表明兼容Mozilla的网站，历史问题，因为以前Mozilla是老大。

Macintosh  苹果的内核，表明我的电脑是苹果系统

Intel Mac OS X 10_10_4  操作系统具体版本及版本号

AppleWebKit/537.36 chrome内核类型与版本，是现在最流行的内核之一，开源。

KHTML, like Gecko KHTML排版引擎，AppleWebKit用的排版引擎WebCore的鼻祖是KHTML。Gecko排版引擎，Firefox的排版引擎。不知为什么这里要写like，有关系吗？难道KHTML是模仿Gecko？呵呵。

Chrome/43.0.2357.134 当前Chrome的版本

Safari/537.36 不知道什么意思，但是Safari是苹果浏览器，而AppleWebKit也是苹果开发用于Safari，因此可能是AppleWebKit需要一部分Safari的功能。

{% highlight bash %}
	Referer:http://192.168.10.214/test
{% endhighlight %}

发送这个请求的页面地址。我们这个请求是在百度首页发出的请求一张图片。故这个参数是百度的网址。
