---
layout: blogs_item
title: Linux下用Shell批量修改文本类型文件格式
author: AcePeak
categories:
  - 积累
tags:
  - 原创
  - shell
  - linux
---

{% highlight bash %}
find ./ -type f -iname '*.txt' | while read i;
do
	echo ${i%.*}
	iconv -f gbk -t utf-8 "`echo ${i%.*}.txt`">"`echo ${i}.tmp`"
	mv "`echo ${i}.tmp`" "`echo ${i%.*}.txt`";
done
{% endhighlight %}
