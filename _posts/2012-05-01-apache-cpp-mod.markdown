---
layout: blogs_item
title: Apache开发C++ Module之一：HelloWorld
author: AcePeak
categories:
  - 积累
tags:
  - Apache
  - C++
  - 原创
---

> 系列列表：
>
> [Apache开发C++ Module之一：HelloWorld]({% post_url 2012-05-01-apache-cpp-mod %})
>
> [Apache开发C++ Module之二：Makefile]({% post_url 2012-05-02-apache-cpp-mod-2 %})


1 首先在[Linux系统安装Apache]({{site.url}}/blogs/2012/04/29/apache-install/)


2 建立初始代码工作区

{% highlight bash  %}
mkdir -p ~/codes/apache/mods/mod_sample/src
cd ~/codes/apache/mods/mod_sample/src
vi mod_sample.c
{% endhighlight %}

3 编写mod_sample.c

{% highlight bash  %}
#include "httpd.h"
#include "http_core.h"
#include "http_protocol.h"
#include "http_request.h"

class Handler
{
public:
	virtual int handle(request_rec* r) = 0;
};

class HelloHandler : public Handler
{
public:
	virtual int handle(request_rec* r)
	{
		// The first thing we will do is write a simple "Hello, world!" back to the client.
		ap_rputs("Hello, world!<br/>", r);
		return OK;
	}
};

/* The handler function for our module.
 * This is where all the fun happens!
 */

static int example_handler(request_rec *r)
{
    /* First off, we need to check if this is a call for the "example" handler.
     * If it is, we accept it and do our things, it not, we simply return DECLINED,
     * and Apache will try somewhere else.
     */
    if (!r->handler || strcmp(r->handler, "example-handler")) return (DECLINED);

	//concrete one handler object and handle the request.
	HelloHandler hh;
	return hh.handle(r);
}

/* register_hooks: Adds a hook to the httpd process */
static void register_hooks(apr_pool_t *pool)
{
    /* Hook the request handler */
    ap_hook_handler(example_handler, NULL, NULL, APR_HOOK_LAST);
}

/* Define our module as an entity and assign a function for registering hooks  */

module AP_MODULE_DECLARE_DATA   example_module =
{
    STANDARD20_MODULE_STUFF,
    NULL,            // Per-directory configuration handler
    NULL,            // Merge handler for per-directory configurations
    NULL,            // Per-server configuration handler
    NULL,            // Merge handler for per-server configurations
    NULL,            // Any directives we may have for httpd
    register_hooks   // Our hook registering function
};

{% endhighlight %}

4 直接使用apxs编译并安装进apache中

{% highlight bash  %}
~/publishes/httpd/bin/apxs -i -a -c -Wc,-lstdc++ -Wc,-xc++ mod_sample.c
{% endhighlight %}

5 修改apache conf文件以设置hello rewrite 映射关系

{% highlight bash  %}
vi ~/publishes/httpd/conf/httpd.conf
{% endhighlight %}

{% highlight xml  %}
</Directory>
<Location "/example">
    SetHandler example-handler
</Location>
{% endhighlight %}

6 重新运行apache以测试接口

{% highlight bash  %}
~/publishes/httpd/bin/apachectl restart
curl http://localhost/example
{% endhighlight %}
