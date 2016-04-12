---
layout: blogs_item
title: Linux琐碎记录之统计源码的行数
author: AcePeak
categories:
  - 积累
tags:
  - Linux
  - 转载
---

Linux下wc命令是统计代码行数的，其用法如下：

{% highlight bash %}
用法：wc [选项]... [文件]...
　或：wc [选项]... --files0-from=F
输出每个指定文件的行数、单词计数和字节数，如果指定了
多于一个文件，继续给出所有相关数据的总计。如果没有指定
文件，或者文件为"-"，则从标准输入读取数据。
  -c, --bytes        输出字节数统计
  -m, --chars        输出字符数统计
  -l, --lines        输出行数统计
      --files0-from=文件    从指定文件读取以NUL 终止的名称，如果该文件被
                    指定为"-"则从标准输入读文件名
  -L, --max-line-length    显示最长行的长度
  -w, --words            显示单词计数
      --help        显示此帮助信息并退出
      --version        显示版本信息并退出
{% endhighlight %}



wc -l *.c *.h 就可以知道当前目录下的所有c 和 h 文件的行数的详细信息。很不错

如果要递归，可以配合其他命令一起使用

当前目录及子目录：

{% highlight bash %}
	find . -name *.c |xargs wc -l
	find . -name *.cpp | xargs wc -l
	find . -name *.h |xargs wc -l
{% endhighlight %}

想一下子 ，或许简单的可以 使用重定向技术 使用

{% highlight bash %}
	find -name "*.c">/tmp/file.list ;find -name "*.h" >>/tmp/file.list;cat /tmp/file.list |xargs wc -l;rm /tmp/file.list
{% endhighlight %}

或者这个比较方便：

{% highlight bash %}
	wc -l `find ./ -name "*.c";find -name "*.h"`|tail -n1
{% endhighlight %}

2.统计文件数量

{% highlight bash %}
	find . -name *.c |wc -l
{% endhighlight %}

3.统计代码行数（过滤空行）

{% highlight bash %}
	find . -name *.c|xargs cat|grep -v ^$|wc -l
{% endhighlight %}



{% highlight bash %}
$ find --help
用法: find [-H] [-L] [-P] [-Olevel] [-D help|tree|search|stat|rates|opt|exec] [path...] [expression]

默认路径为当前目录；默认表达式为 -print
表达式可能由下列成份组成：操作符、选项、测试表达式以及动作：

操作符 (优先级递减；未做任何指定时默认使用 -and):
      ( EXPR )   ! EXPR   -not EXPR   EXPR1 -a EXPR2   EXPR1 -and EXPR2
      EXPR1 -o EXPR2   EXPR1 -or EXPR2   EXPR1 , EXPR2

位置选项 (总是真): -daystart -follow -regextype

普通选项 (总是真，在其它表达式前指定):
      -depth --help -maxdepth LEVELS -mindepth LEVELS -mount -noleaf
      --version -xdev -ignore_readdir_race -noignore_readdir_race

测试(N可以是 +N 或-N 或 N):-amin N -anewer FILE -atime N -cmin  
      -cnewer 文件 -ctime N -empty -false -fstype 类型 -gid N -group 名称
      -ilname 匹配模式 -iname 匹配模式 -inum N -ipath 匹配模式 -iregex 匹配模式
      -links N -lname 匹配模式 -mmin N -mtime N -name 匹配模式 -newer 文件
      -nouser -nogroup -path 匹配模式 -perm [+-]访问模式 -regex 匹配模式
      -readable -writable -executable
      -wholename PATTERN -size N[bcwkMG] -true -type [bcdpflsD] -uid N
      -used N -user NAME -xtype [bcdpfls]

动作: -delete -print0 -printf FORMAT -fprintf FILE FORMAT -print
      -fprint0 FILE -fprint FILE -ls -fls FILE -prune -quit
      -exec COMMAND ; -exec COMMAND {} + -ok COMMAND ;
      -execdir COMMAND ; -execdir COMMAND {} + -okdir COMMAND ;

通过 findutils 错误报告页 http://savannah.gnu.org/ 报告错误及跟踪修定过程。如果您无法浏览网页，请发电子邮件至 <bug-findutils@gnu.org>。
{% endhighlight %}
