---
layout: blogs_item
title: Hadoop1.2.1系统分布式配置
author: AcePeak
categories: [Internet]
tags: 
- Web
- Hadoop
---


环境：CentOS6.5、hadoop1.2.1、jdk1.8.0

namenode:centos1(ip:172.16.26.129)

datanode:centos2(ip:172.16.26.130)、centos3(ip:172.16.26.131)



配置步骤：

（1）在所有机器上安装所需软件

{% highlight shell %}
[root@centos1 ~] # yum -y install wget, java-1.8.0-openjdk-devel, ssh
{% endhighlight %}


（2）在所有机器上配置NameNode和DataNode


在所有机器上修改/etc/hosts

{% highlight shell %}
[root@centos1 ~] # vi /etc/hosts

127.0.0.1               localhost.localdomain localhost centos1
172.16.26.129             centos1
172.16.26.130             centos2
172.16.26.131             centos3
::1             localhost6.localdomain6 localhost6 centos1
{% endhighlight %}


在所有机器上修改hostname

{% highlight shell %}
[root@centos1 ~] # hostname centos1
[root@centos1 ~] # hostname
centos1
{% endhighlight %}


在所有机器上修改network配置

{% highlight shell %}
[root@centos1 ~] # vi /etc/sysconfig/network			//修改HOSTNAME＝XXX
{% endhighlight %}


在所有机器上关闭防火墙

{% highlight shell %}
[root@centos1 ~] # service iptables stop
[root@centos1 ~] # service iptables status
{% endhighlight %}


(3)在所有机器上建立相同的用户

在所有机器上成功建立grid用户后，设置用户密码

{% highlight shell %}
[root@centos1 ~] # useradd grid
[root@centos1 ~] # passwd grid
{% endhighlight %}


（4）在namenode上设置SSH无密码访问

在所有机器上使用grid用户登录

{% highlight shell %}
[root@centos1 ~] # su grid
{% endhighlight %}


在所有机器上/home/grid下创建ssh文件夹

{% highlight shell %}
[grid@centos2 ~] $ mkdir .ssh
{% endhighlight %}


在namenode上生成密钥对

{% highlight shell %}
[grid@centos1 ~] $ ssh-keygen -t dsa -P '' -f ~/.ssh/id_dsa
[grid@centos1 ~] $ cat ~/.ssh/id_dsa.pub >> ~/.ssh/authorized_keys
{% endhighlight %}


> 注意点：
> 
> 不进行以下步骤SSH免密码登录设置会不成功
> 
> .ssh目录要设成700 有执行权限
> authorized_keys要设成600 否则会出错
> 还有ssh 登陆要加入用户名的 比如
> ssh root@localhost
> 
> 这时从centos1向其他机器发起SSH连接，只有第一次登录时需要输入密码，以后则不需要


(5)在所有机器上安装配置hadoop1.2.1

首先在namenode上配置，配置后在分发到datanode上

{% highlight shell %}
[grid@centos1 ~] $ wget http://mirror.bit.edu.cn/apache/hadoop/common/hadoop-1.2.1/hadoop-1.2.1.tar.gz
[grid@centos1 ~] $ tar -xf hadoop-1.2.1.tar.gz 
[grid@centos1 ~] $ cd hadoop-1.2.1
{% endhighlight %}


接下来需要修改hadoop的conf文件夹下的配置信息：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi conf/hadoop-env.sh
export JAVA_HOME=/usr/java/jvm/java
{% endhighlight %}


修改core-site.xml，如下：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi conf/core-site.xml
<configuration>
<property>
<name>fs.default.name</name>
<value>hdfs://centos1:9000</value>
</property>
<property>
<name>hadoop.tmp.dir</name>
<value>/home/grid/tmp</value>
</property>
</configuration>
{% endhighlight %}


> 注意：hadoop.tmp.dir是hadoop文件系统依赖的基础配置，很多路径都依赖它。它默认的位置是在/tmp/{$user}下面，在local和hdfs都会建有相同的目录，但是在/tmp路径下的存储是不安全的，因为linux一次重启，文件就可能被删除。导致namenode启动不起来。


修改hdfs-site.xml，如下

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi conf/hdfs-site.xml
<configuration>
<property>
<name>dfs.replication</name>
<value>1</value>
</property>
</configuration>
{% endhighlight %}


修改mapred-site.xml，如下（保险起见这里写centos1对应的IP地址）：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi conf/mapred-site.xml
<configuration>
<property>
<name>mapred.job.tracker</name>
<value>172.16.26.129:9001</value>
</property>
</configuration>
{% endhighlight %}


masters里写入作为namenode节点机器的IP

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi conf/masters
172.16.26.129
{% endhighlight %}


slaves里写入作为datanode节点的机器的IP

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi conf/slaves
172.16.26.130
172.16.26.131
{% endhighlight %}


修改bin下的hadoop中Jvm的调用方式

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ vi bin/hadoop
{% endhighlight %}


查找 –jvm . vi 下的命令模式： :/-jvm，将-jvm server改成 –server .

> 因为JDK1.6已经废除了一个参数-jvm,如果不修改的话，无法启动数据节点。


到此，hadoop的有关配置已经完成，namenode端通过如下命令把配置好的hadoop发送到各个datanode处：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ scp -r ~/hadoop-1.2.1 centos2:/home/grid
[grid@centos1 hadoop-1.2.1] $ scp -r ~/hadoop-1.2.1 centos3:/home/grid
{% endhighlight %}


（6）启动服务

在namenode端格式化分布式文件系统：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/hadoop namenode -format
{% endhighlight %}


如果没有任何error字样的信息，下面接着在namenode端启动hadoop进程：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/start-all.sh
{% endhighlight %}


如果没有其它差错的话，hadoop可以正常启动，并能够在各个机器上得到验证：


在namenode端用jps命令查看启动情况，如下：

{% highlight shell %}
[grid@centos1 ~] $ jps
xxxx Jps
xxxx Namenode
xxxx Secondarynamenode
xxxx JobTracker
{% endhighlight %}


在datanode端用jps查看启动情况，如下：

{% highlight shell %}
[grid@centos2 ~] $ jps
xxxx Jps
xxxx DataNode
xxxx TaskTracker
{% endhighlight %}


然后可以通过如下地址来查看集群运行状况：

{% highlight shell %}
    http://172.16.26.129:50030
    http://172.16.26.129:50070
    http://172.16.26.130:50060
    http://172.16.26.131:50060
{% endhighlight %}


-------------------------------------我是分割线-------------------------------


跑hadoop自带的wordcount程序


1、通过hadoop的命令在HDFS上创建/tmp/workcount目录，命令如下：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/hadoop fs -mkdir /tmp/wordcount
{% endhighlight %}


2、通过copyFromLocal命令把本地的word.txt复制到HDFS上，命令如下：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/hadoop fs -copyFromLocal /home/grid/word.txt  /tmp/wordcount/word.txt
{% endhighlight %}

 

3、通过命令运行例子，使用命令如下：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/hadoop jar hadoop-examples-1.2.1.jar wordcount /tmp/wordcount/word.txt  /tmp/wordcount/out
{% endhighlight %}


4、查看运行结果，查看例子的输出结果使用命令： 

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/hadoop fs -ls /tmp/wordcount/out
{% endhighlight %}


发现有两个文件夹和一个文件，使用命令查看part-r-00000文件：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ bin/hadoop fs -cat /tmp/wordcount/out/part-r-00000
{% endhighlight %}


-------------------------------------我是分割线-------------------------------


问题1：

namenode无法启动，启动显示host = java.net.UnknownHostException


应对：

针对每台机器需要设置正确的hostname，方法如下：

{% highlight shell %}
[grid@centos1 hadoop-1.2.1] $ su
[root@centos1 hadoop-1.2.1] # vi /etc/sysconfig/network			//修改HOSTNAME＝XXX
[root@centos1 hadoop-1.2.1] # vi /etc/hosts						//修改映射关系从跟本机有关的IP映射到XXX
[root@centos1 hadoop-1.2.1] # hostname XXX
[root@centos1 hadoop-1.2.1] # service network restart
[root@centos1 hadoop-1.2.1] # su grid
[grid@centos1 hadoop-1.2.1] # bin/start-all.sh
{% endhighlight %}


问题2：

datanode无法启动，报错NoRouteToHostException: No route to host


应对：

关闭master的防火墙。


问题3：

ssh无法无密码访问，每次都需要输入密码


应对：
暂时还没有更好的解决方法！

