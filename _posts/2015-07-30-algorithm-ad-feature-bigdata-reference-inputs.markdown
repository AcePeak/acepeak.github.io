---
layout: blogs_item
title: 广告特征工程+人工智能：大数据结果引入并特征相关化（二）
author: AcePeak
categories:
  - 深度
tags:
  - 原创
  - DSP
  - DMP
  - 算法
---

> 系列列表：
>
> [广告特征工程+人工智能：在线程序化特征定义（一）]({{site.url}}/blogs/2012/07/28/algorithm-ad-feature-online-feature-definition/)
>
> [广告特征工程+人工智能：大数据结果引入并特征相关化（二）]({{site.url}}/blogs/2012/07/30/algorithm-ad-feature-bigdata-reference-inputs/)
>
> [广告特征工程+人工智能：特征历史数据指导特征计算（三）]({{site.url}}/blogs/2012/08/01/algorithm-ad-feature-history-teach/)


#大数据结果引入并特征相关化

1 平均年龄：微型轿车33.3，小型轿车33.6，紧凑型轿车34.6，中型轿车35.1，中大型轿车37.0，轿车34.4，SUV35.6，MPV35.3

{% highlight bash %}
from $SOURCE, at $TIME, MEAN(F1|F2)=33.3
from $SOURCE, at $TIME, MEAN(F1|F3)=33.6
from $SOURCE, at $TIME, MEAN(F1|F4)=34.6
from $SOURCE, at $TIME, MEAN(F1|F5)=35.1
from $SOURCE, at $TIME, MEAN(F1|F6)=37.0
from $SOURCE, at $TIME, MEAN(F1|F7)=34.4
from $SOURCE, at $TIME, MEAN(F1|F8)=35.6
from $SOURCE, at $TIME, MEAN(F1|F9)=35.3
{% endhighlight %}


2 性别比例：微型轿车（男性50.3%，女性49.7%），小型轿车（55.1%，44.9%），紧凑型轿车（56.7%，43.3%），中型轿车（61.3%，38.7%），中大型轿车（64.3%，35.7%），轿车（56.9%，43.1%），SUV（74.1%，25.9%），MPV（77.7%，22.3%）

{% highlight bash %}
from $SOURCE, at $TIME, P(F10,F2)/P(F2)=50.3%
from $SOURCE, at $TIME, P(F10,F3)/P(F3)=55.1%
from $SOURCE, at $TIME, P(F10,F4)/P(F4)=56.7%
from $SOURCE, at $TIME, P(F10,F5)/P(F5)=61.3%
from $SOURCE, at $TIME, P(F10,F6)/P(F6)=64.3%
from $SOURCE, at $TIME, P(F10,F7)/P(F7)=56.9%
from $SOURCE, at $TIME, P(F10,F8)/P(F8)=74.1%
from $SOURCE, at $TIME, P(F10,F9)/P(F9)=77.7%,
{% endhighlight %}

3 婚姻状况：微型轿车（已婚有子女64.7%，已婚无子女11.6%，未婚23.7%），小型轿车（61.0%，19.9%，19.0%），紧凑型轿车（68.5%，13.9%，17.5%）

{% highlight bash %}
from $SOURCE, at $TIME, P(F12,F15,F2)/P(F2)=64.7%
from $SOURCE, at $TIME, P(F12,F16,F2)/P(F2)=11.6%
from $SOURCE, at $TIME, P(F12,F15,F3)/P(F3)=61.0%
from $SOURCE, at $TIME, P(F12,F16,F3)/P(F3)=19.9%
{% endhighlight %}

4 家庭人数：轿车（3.07人），SUV（3.11人），MPV（3.20人）

{% highlight bash %}
from $SOURCE, at $TIME, MEAN(F17|F7)=3.07
from $SOURCE, at $TIME, MEAN(F17|F8)=3.11
from $SOURCE, at $TIME, MEAN(F17|F9)=3.20
{% endhighlight %}

5 最高学历：微型轿车（高中及以下35.5%，大专40.9%，本科22.7%），中大型轿车（19.5%，34.6%，43.6%）

{% highlight bash %}
from $SOURCE, at $TIME, P(F18,F2)/P(F2)=35.5%
from $SOURCE, at $TIME, P(F19,F2)/P(F2)=40.9%
from $SOURCE, at $TIME, P(F20,F2)/P(F2)=22.7%
from $SOURCE, at $TIME, P(F18,F6)/P(F6)=19.5%
from $SOURCE, at $TIME, P(F19,F6)/P(F6)=34.6%
from $SOURCE, at $TIME, P(F20,F2)/P(F6)=43.6%
{% endhighlight %}

6 所在行业：零售批发（微型15.8%，中大型轿车8.7%，SUV12.9%），贸易进出口（微型5.6%，中大型11.3%，SUV9.3%）

{% highlight bash %}
from $SOURCE, at $TIME, P(F22,F2)=15.8%
from $SOURCE, at $TIME, P(F22,F6)=8.7%
from $SOURCE, at $TIME, P(F22,F8)=12.9%
{% endhighlight %}

7 职业：雇员人数在20人及以上的企业业主（微型3.8%，中大型14.7%，SUV5.9%），外资企业高级管理人员（微型0.8%，中大型4.5%，SUV3.2%）

{% highlight bash %}
from $SOURCE, at $TIME, P(F32,F27,F2)=3.8%
from $SOURCE, at $TIME, P(F32,F27,F6)=14.7%
from $SOURCE, at $TIME, P(F32,F27,F8)=5.9%
from $SOURCE, at $TIME, P(F29,F26,F2)=0.8%
from $SOURCE, at $TIME, P(F29,F26,F6)=4.5%
from $SOURCE, at $TIME, P(F29,F26,F8)=3.2%)
{% endhighlight %}

8 个人家庭收入：微型轿车（个人5728，家庭11821），中大型轿车（个人20225，家庭37705），SUV（11206，19536）

{% highlight bash %}
from $SOURCE, at $TIME, MEAN(F34|F2)=5728
from $SOURCE, at $TIME, MEAN(F35|F2)=11821
from $SOURCE, at $TIME, MEAN(F34|F6)=20225
from $SOURCE, at $TIME, MEAN(F35|F6)=37705
{% endhighlight %}

9 购车动机：在接受调查的人中，上下班方便（微型86.7%，中大型轿车71.4%，SUV70.9%）

{% highlight bash %}
from $SOURCE, at $TIME, P(F36,F38,F2)/P(F38)=86.7%
from $SOURCE, at $TIME, P(F36,F38,F6)/P(F38)=71.4%
{% endhighlight %}

10 油耗：微型车（不开空调6.7，开空调7.9），中大型轿车（11.0，12.3）

{% highlight bash %}
from $SOURCE, at $TIME, MEAN(F45|F47)=6.7
from $SOURCE, at $TIME, MEAN(F46|F47)=7.9
from $SOURCE, at $TIME, MEAN(F45|F51)=11.0
from $SOURCE, at $TIME, MEAN(F46|F51)=12.3
{% endhighlight %}


#特征历史数据指导特征计算
