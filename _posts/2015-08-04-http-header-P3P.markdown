---
layout: blogs_item
title: HTTP请求头系列（2）-P3P
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


对于IE来说(默认安全级别下)，iframe、img、link等标签都是只发送session cookie（又叫 第一方cookie），拦截本地cookie发送（又叫第三方cookie）。当这些标签跨域引用一个页面，实际上是发起了一次GET请求。

如果这个跨域的请求，HTTP返回头中带有Set-Cookie ， 那么这个cookie对浏览器来说，实际上是无效的。

看如下测试

假设有 www.a.com    与 www.b.com 两个域

在 www.b.com 上有一个页面，其中包含一个指向 www.a.com 的iframe

http://www.b.com/test.html 的内容为：

{% highlight html %}
<iframe width=300 height=300 src="http://www.a.com/test.php" ></iframe>
{% endhighlight %}


http://www.a.com/test.php 是一个对 a.com 域设置 cookie的页面，其内容为：

{% highlight php %}
<?php
header("Set-Cookie: test=axis; domain=.a.com; path=/");
?>
<script>
    alert(document.cookie);
</script>
{% endhighlight %}


此时我们请求 http://www.b.com/test.html , 他包含一个iframe，会去跨域请求 www.a.com/test.php ，该php页面会尝试 set-cookie

第一次请求， test.php 会 set-cookie，所以浏览器会收到一个cookie。

如果 set-cookie 成功，再次请求该页面，浏览器应该会 sent 刚才 recieve 到的cookie。可是由于前面说的跨域限制，在IE里的iframe标签是 set-cookie不成功的，所以无法sent刚才收到的cookie。 这里无论是 session cookie 还是本地cookie都是一样。


可以看到，第二次发包，还是没能sent出去cookie

但是这种情况在加入了P3P header 后会改变。

P3P header允许跨域访问隐私数据，从而可以跨域set-cookie成功

我们修改 www.a.com/test.php 为

{% highlight php %}
<?php
header("P3P: CP=CURa ADMa DEVa PSAo PSDo OUR BUS UNI PUR INT DEM STA PRE COM NAV OTC NOI DSP COR");
header("Set-Cookie: test=axis; expires=Sun, 23-Dec-2018 08:13:02 GMT; domain=.a.com; path=/");
?>
<script>
    alert(document.cookie);
</script>
{% endhighlight %}


再次访问两次上面的测试过程



可以看到第二个包已经发送出了收到的cookie

而我们写的javascript也能够弹出cookie了。


值得注意的是，P3P header只需要设置一次，这样跟在这个P3P header后面的所有 set-cookie，都可以跨域访问了。也就是说: 被P3P header设置过一次后，之后的请求不再需要P3P header，也能够在iframe里跨域发送这些cookie。

但是如果用 set-cookie 去改变设置好的cookie，则不再具有这种跨域访问特性。


P3P header 还有一个特点就是同一个包里只能设置一次，后面的P3P Header不会覆盖前面的P3P header，浏览器只认第一个。

P3P 是 The Platform for Privacy Preferences 的简称

更多具体的内容可以参阅W3C的标准 [http://www.w3.org/TR/P3P/](http://www.w3.org/TR/P3P/)

在这里，我们看到的很乱的 P3P header里的东西，都不知道是什么乱七八糟的策略内容，实际上这是一些简写

比如 上面用到的

{% highlight bash %}
P3P: CP=CURa ADMa DEVa PSAo PSDo OUR BUS UNI PUR INT DEM STA PRE COM NAV OTC NOI DSP COR
{% endhighlight %}

CP 是 Compact Policy 的简写

CURa 中 CUR 是 <current/> 的简写， a 是 always 的简写

当然P3P header也可以直接 引用一个 xml 策略文件

比如这么写

{% highlight bash %}
HTTP/1.1 200 OK
P3P: policyref="http://catalog.example.com/P3P/PolicyReferences.xml"
Content-Type: text/html
Content-Length: 7413
Server: CC-Galaxy/1.3.18
{% endhighlight %}


使用P3P的方法还有很多，这里不一一列举了。


最后，利用P3P Header 的这种特性，在实际攻击中，还是可以利用一下的。

比如利用CRLF插入一个P3P header后，改变一个本地cookie的值，该cookie在之后的过程中可以被iframe引用到，也许会发生一些很奇妙的事情。

具体会变成什么样我也不知道，毕竟web应用安全和环境的关系是越来越紧密了。
