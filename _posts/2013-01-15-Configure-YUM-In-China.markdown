---
layout: blogs_item
title: 在国内配置Yum源的方法
author: AcePeak
categories: [Internet]
tags: 
- 原生
- Linux
---

系统默认的yum 源速度往往不尽人意，为了达到快速安装的目的，在这里修改yum源为国内源。

上海交通大学yum源

a. 修改/etc/yum.repos.d/CentOS-Base.repo为：


{% highlight python %}
# CentOS-Base.repo
#
# The mirror system uses the connecting IP address of the client and the
# update status of each mirror to pick mirrors that are updated to and
# geographically close to the client.  You should use this for CentOS updates
# unless you are manually picking other mirrors.
#
# If the mirrorlist= does not work for you, as a fall back you can try the 
# remarked out baseurl= line instead.
#
#

[base]
name=CentOS-$releasever - Base
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
baseurl=http://ftp.sjtu.edu.cn/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#released updates 
[updates]
name=CentOS-$releasever - Updates
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
baseurl=http://ftp.sjtu.edu.cn/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
baseurl=http://ftp.sjtu.edu.cn/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#additional packages that extend functionality of existing packages
[centosplus]
name=CentOS-$releasever - Plus
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus
baseurl=http://ftp.sjtu.edu.cn/centos/$releasever/centosplus/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5

#contrib - packages by Centos Users
[contrib]
name=CentOS-$releasever - Contrib
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib
baseurl=http://ftp.sjtu.edu.cn/centos/$releasever/contrib/$basearch/
gpgcheck=1
enabled=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-5
{% endhighlight %}


或者可以到这个链接下载：
[CentOS-Base.repo](/file/CentOS-Base.repo)


关于变量


$releasever：代表发行版的版本，从[main]部分的distroverpkg获取，如果没有，则根据redhat-release包进行判断。

$arch：cpu体系，如i686,athlon等

$basearch：cpu的基本体系组，如i686和athlon同属i386，alpha和alphaev6同属alpha。


b. 导入GPG KEY

yum 可以使用gpg 对包进行校验，确保下载包的完整性，所以我们先要到各个repository 站点找到gpg key，一般都会放在首页的醒目位置，一些名字诸如RPM-GPG-KEY-CentOS-5 之类的纯文本文件，把它们下载下来，然后用rpm --import RPM-GPG-KEY-CentOS-5 命令将key 导入。


c. 执行yum 命令



其他国内yum源列表如下：

1. 企业贡献：

搜狐开源镜像站：http://mirrors.sohu.com/

网易开源镜像站：http://mirrors.163.com/

2. 大学教学：

北京理工大学：

http://mirror.bit.edu.cn (IPv4 only)

http://mirror.bit6.edu.cn (IPv6 only)

北京交通大学：

http://mirror.bjtu.edu.cn (IPv4 only)

http://mirror6.bjtu.edu.cn (IPv6 only)

http://debian.bjtu.edu.cn (IPv4+IPv6)

兰州大学：http://mirror.lzu.edu.cn/

厦门大学：http://mirrors.xmu.edu.cn/

清华大学：

http://mirrors.tuna.tsinghua.edu.cn/ (IPv4+IPv6)

http://mirrors.6.tuna.tsinghua.edu.cn/ (IPv6 only)

http://mirrors.4.tuna.tsinghua.edu.cn/ (IPv4 only)

天津大学：http://mirror.tju.edu.cn/

中国科学技术大学：

http://mirrors.ustc.edu.cn/ (IPv4+IPv6)

http://mirrors4.ustc.edu.cn/

http://mirrors6.ustc.edu.cn/

东北大学：

http://mirror.neu.edu.cn/ (IPv4 only)

http://mirror.neu6.edu.cn/ (IPv6 only)

电子科技大学：http://ubuntu.uestc.edu.cn/

