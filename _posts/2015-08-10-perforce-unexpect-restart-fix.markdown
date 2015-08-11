---
layout: blogs_item
title: Perforce意外重启后无法启动的问题
author: AcePeak
categories: [Internet]
tags: 
- 原生
- Perforce
---


1 首先删除p4.protect，备份并删除p4.counters

{% highlight bash %}
rm -rf p4.protect
mv p4.counters p4.counters.bak
{% endhighlight %}

2 备份用户信息文件并删除

{% highlight bash %}
mv p4.users p4.users.bak
{% endhighlight %}

3 重启perforce服务

{% highlight bash %}
services perforce start
{% endhighlight %}

4 连接Perforce服务器并建立新用户

{% highlight bash %}
./p4v.exe
new user aaa //密码需要符合要求，如大小写+数字+8位以上
{% endhighlight %}

5 以新用户登录进入Perforce Admin并成为sole administrator

{% highlight bash %}
login aaa
admin login aaa as sole administrator
{% endhighlight %}

6 在Perforce Admin中重新创建所有用户并进行权限重新设置

{% highlight bash %}
user create xxx
user permission xxx
{% endhighlight %}

7 打开命令行工具，根据p4.counters.bak中的key和value进行p4 counter update

{% highlight bash %}
//example: change 1576; maxCommitChange 1576; upgrade 1576;
p4 -C utf8 counter -f change 1576
p4 -C utf8 counter -f maxCommitChange 1576
{% endhighlight %}
