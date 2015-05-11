---
layout: blogs_item
title: Linux系统安装Apache
author: AcePeak
categories: [Internet]
tags: 
- Apache
- Web
---


1 首先安装[APR](http://apr.apache.org/)

{% highlight bash  %}
mkdir -p ~/codes/apache/apr/
cd ~/codes/apache/apr/
wget http://apache.mirror.cdnetworks.com//apr/apr-1.5.2.tar.gz
tar -xf apr-1.5.2.tar.gz
cd apr-1.5.2
mkdir -p ~/publishes/apr/
./configure --prefix=`echo ~`/publishes/apr/
make
make install
{% endhighlight %}


1 安装[APR-Util](http://apr.apache.org/)

{% highlight bash  %}
mkdir -p ~/codes/apache/apr-util/
cd ~/codes/apache/apr-util/
wget http://apache.mirror.cdnetworks.com//apr/apr-util-1.5.4.tar.gz
tar -xf apr-util-1.5.4.tar.gz
cd apr-util-1.5.4
mkdir -p ~/publishes/apr-util/
./configure --prefix=`echo ~`/publishes/apr-util/ --with-apr=`echo ~`/publishes/apr/
make
make install
{% endhighlight %}


3 安装[Pcre](http://www.pcre.org/)

{% highlight bash  %}
mkdir -p ~/codes/apache/pcre/
cd ~/codes/apache/pcre/
wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.37.tar.gz
tar -xf pcre-8.37.tar.gz
cd pcre-8.37
mkdir -p ~/publishes/pcre/
./configure --prefix=`echo ~`/publishes/pcre/
make
make install
{% endhighlight %}


4 安装[Apache](http://httpd.apache.org/)

{% highlight bash  %}
mkdir -p ~/codes/apache/httpd/
cd ~/codes/apache/httpd/
wget http://apache.tt.co.kr//httpd/httpd-2.4.12.tar.gz
tar -xf httpd-2.4.12.tar.gz
cd httpd-2.4.12
mkdir -p ~/publishes/httpd/
./configure --prefix=`echo ~`/publishes/httpd/ --with-apr=`echo ~`/publishes/apr --with-apr-util=`echo ~`/publishes/apr-util --with-pcre=`echo ~`/publishes/pcre
make
make install
{% endhighlight %}

5 启动Apache

{% highlight bash  %}
~/publishes/httpd/bin/apachectl start 
curl http://localhost
{% endhighlight %}
