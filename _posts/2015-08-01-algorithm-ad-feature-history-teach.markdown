---
layout: blogs_item
title: 广告特征工程+人工智能：特征历史数据指导特征计算（三）
author: AcePeak
categories: [广告平台]
tags: 
- 原生
- DSP
- 算法
---

> 系列列表：
> 
> [广告特征工程+人工智能：在线程序化特征定义（一）]({{site.url}}/blogs/2012/07/28/algorithm-ad-feature-online-feature-definition/)
> 
> [广告特征工程+人工智能：大数据结果引入并特征相关化（二）]({{site.url}}/blogs/2012/07/30/algorithm-ad-feature-bigdata-reference-inputs/)
> 
> [广告特征工程+人工智能：特征历史数据指导特征计算（三）]({{site.url}}/blogs/2012/08/01/algorithm-ad-feature-history-teach/)

#特征历史数据指导特征计算

##按照概率的计算方式

假设用户A已经拥有如下标签：**F10男性**，**F12已婚**，**F16无子女**，**F20本科**
 
待投的广告有2个：**微型轿车**、**大中型轿车**

那么我们将市场平均概率与该人的相应实际情况进行比较，也就是市场概率即此人的购车期望与此人的目前实际情况进行比较，涉及到期望的数据为：

与待投广告有关的市场期望标签：**F2=用户.轿车.Exists(轿车.cat=微型)**,**F6=用户.轿车.Exists(轿车.cat=中大型)**

根据往年历史调研，与此有关的几项数据有：

{% highlight bash %}
P(F10,F2)/P(F2)=50.3%
P(F10,F6)/P(F6)=64.3%
P(F12,F16,F2)/P(F2)=11.6%
P(F20,F2)/P(F2)=22.7%
P(F20,F2)/P(F6)=43.6%
{% endhighlight %}

那么分别计算此人对某广告的期望与实际情况：

{% highlight bash %}
P(F10,F12,F16,F20,F2)为有车概率
P(F10,F12,F16,F20)或P(F10,F12,F16,F20,^F2)为无车的概率
{% endhighlight %}

那么我们是需要计算
{% highlight bash %}
P(F10,F12,F16,F20,F2)=1-^P
=1-^P(F10)|^P(F12)|^P(F16)|^P(F20)|^P(F2)
=1-^P(F10,F2)|^P(F12,F16)|^P(F20)
=1-(1-P(F10,F2))|
{% endhighlight %}


##按照均值的计算方式




##来源的影响




##时间的影响





