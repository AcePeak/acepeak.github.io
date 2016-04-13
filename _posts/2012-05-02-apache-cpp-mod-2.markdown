---
layout: blogs_item
title: Apache开发C++ Module之二：Makefile
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

1 创建.dep文件

{% highlight bash  %}
touch .deps
{% endhighlight %}

2 创建modules.mk文件

{% highlight basemake  %}
DISTCLEAN_TARGETS = modules.mk
static =
shared =
{% endhighlight %}

3 写Makefile文件

{% highlight basemake  %}
top_srcdir   = ~/codes/apache/httpd/httpd-2.4.12
top_builddir = ~/codes/apache/httpd/httpd-2.4.12
srcdir       = ./src
builddir     = .
VPATH        = .
# a modules Makefile has no explicit targets -- they will be defined by
# whatever modules are enabled. just grab special.mk to deal with this.
include $(top_srcdir)/build/special.mk

APXS=~/publishes/httpd/bin/apxs
MODULE = src/mod_sample.la
SOURCES = src/mod_sample.c
FILEDEPS =
CC_FLAGS=$(shell apxs -q CFLAGS) $(shell apr-1-config --cppflags) -I./src -I/usr/include/httpd
LD_FLAGS=-Wl$(shell pkg-config --libs protobuf) $(shell apr-1-config --libs)

all: $(MODULE)

debug:
	$(APXS) -S CC=g++ -S CFLAGS="$(CC_FLAGS) -D_DEBUG -g -O0" $(LD_FLAGS) -c $(SOURCES)

$(MODULE): $(SOURCES)
	$(APXS) -S CC=g++ -S CFLAGS="$(CC_FLAGS)" $(LD_FLAGS) -c $(SOURCES)

install: all
	$(APXS) -i $(MODULE) /usr/local/lib/libprotobuf.a
	apachectl restart

clean:
	@rm $(MODULE) src/*.o src/*.lo src/*.slo *.o src/gpb/*o
{% endhighlight %}
