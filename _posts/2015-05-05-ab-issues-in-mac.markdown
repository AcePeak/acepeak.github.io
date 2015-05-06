---
layout: blogs_item
title: MacOSX上ab并发测试常见报错及解决办法
author: AcePeak
categories: [Internet]
tags: 
- Web
---

> 1、apr_socket_recv: Connection reset by peer (54)


{% highlight bash  %}
Mac:~ air$ ab -n 10000 -c 2000 http://127.0.0.1:80/
This is ApacheBench, Version 2.3 &lt;$Revision: 655654 $&gt;
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 127.0.0.1 (be patient)
apr_socket_recv: Connection reset by peer (54)
Mac:~ air$
{% endhighlight %}


这个报错一般是由于使用的MacOSX默认自带的ab限制了并发数导致的。

解决办法：

下载最新的apache并重新编译，备份原来的ab并将新编译的ab替换到原来的路径


{% highlight bash  %}
$ ./configure --prefix=/usr/local/webserver/httpd-2.4.10
$ make
$ make install
$ cd /usr/local/webserver/httpd-2.4.10
$ sudo mv /usr/sbin/ab /usr/sbin/ab.bak
$ sudo cp bin/ab /usr/sbin/ab
{% endhighlight %}


> 2、socket: Too many open files (24)


一般这种报错是由于MacOSX默认的open files数值过小导致的。
查看当前系统的默认文件打开数：


{% highlight bash  %}
$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
file size               (blocks, -f) unlimited
max locked memory       (kbytes, -l) unlimited
max memory size         (kbytes, -m) unlimited
open files                      (-n) 256
pipe size            (512 bytes, -p) 1
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 709
virtual memory          (kbytes, -v) unlimited
{% endhighlight %}


可以看到默认的open files数值为256，解决办法将此数值调大即可。
先查看以下两个数值：


{% highlight bash  %}
$ sysctl kern.maxfiles
kern.maxfiles: 50000
$ sysctl kern.maxfilesperproc
kern.maxfilesperproc: 50000
{% endhighlight %}


要修改成的数值不能大于以上两个数值，如果直接执行ulimit -n 65535则会报以下错误：


{% highlight bash  %}
-bash: ulimit: open files: cannot modify limit: Operation not permitted
{% endhighlight %}


所以执行以下命令：


{% highlight bash  %}
ulimit -n 49999
{% endhighlight %}


或者直接调大上述两个配置的数值：


{% highlight bash  %}
$ sudo sysctl -w kern.maxfiles=1048600
$ sudo sysctl -w kern.maxfilesperproc=1048576
{% endhighlight %}


继续ab测试：

{% highlight bash  %}
ab -n 10000 -c 2000 http://127.0.0.1:80/
{% endhighlight %}

现在应该一切OK了