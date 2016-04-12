---
layout: blogs_item
title: 广告特征工程+人工智能：在线程序化特征定义（一）
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

#在线程序化特征定义

例子，请参考[新华信2011年上半年的研究报告](http://wenku.baidu.com/link?url=G3GSS98khJorXesmyl1uWMq-EHJgFyngkn-w6xxZEshkwJ6unOqs-5QZa5JGek37Ye8N3UD4zGA5G7IkjJ6DmLGfvYR3rwNN2d86kt9K_B3)


{% highlight bash %}
TIME＝2011HY1
SOURCE＝XINHUAXIN

[Data]
F1=用户.年龄
F17=用户.子女.count
F34=用户.月均税前收入
F35=用户.月均税前收入+用户.配偶.月均税前收入
F45=轿车.调研.平均油耗不开空调
F46=轿车.调研.平均油耗开空调
F54=用户.轿车.满意度


[Feature]
F2=用户.轿车.Exists(轿车.cat=微型)
F3=用户.轿车.Exists(轿车.cat=小型)
F4=用户.轿车.Exists(轿车.cat=紧凑型)
F5=用户.轿车.Exists(轿车.cat=中型)
F6=用户.轿车.Exists(轿车.cat=中大型)
F7=用户.轿车.count>0
F8=用户.轿车.Exists(轿车.type=SUV)
F9=用户.轿车.Exists(轿车.type=MPV)
F10=用户.性别＝＝男性
F11=用户.性别＝＝女性
F12=用户.已婚
F13=用户.未婚
F14=用户.离异
F15=用户.子女.count>0
F16=用户.子女.count=0
F18=用户.学历<＝高中及以下
F19=用户.学历＝＝大专
F20=用户.学历＝＝本科
F21=用户.学历>＝硕士
F22=用户.行业.Exists(行业.cat=零售批发)
F23=用户.行业.Exists(行业.cat=贸易进出口)
F24=用户.职业.当前.职级＝＝一般
F25=用户.职业.当前.职级＝＝中级管理
F26=用户.职业.当前.职级＝＝高级管理
F27=用户.职业.当前.职级＝＝所有者
F28=用户.职业.当前.单位.性质＝＝私营企业
F29=用户.职业.当前.单位.性质＝＝外资企业
F30=用户.职业.当前.单位.性质＝＝国营集体企业
F31=用户.职业.当前.单位.性质＝＝政府机关事业单位
F32=用户.职业.当前.单位.人数>=20
F33=用户.职业.当前.单位.人数<20
F36=调研.用户.购车动机.Contains(上下班方便)
F37=调研.用户.购车动机.Contains(与客户打交道时获得信任)
F38=调研.用户.购车动机.count>0
F39=调研.用户.购车考虑因素.Contains(外观)
F40=调研.用户.购车考虑因素.Contains(安全性)
F41=调研.用户.车辆使用用途.Contains(上下班代步)
F42=调研.用户.车辆使用用途.Contains(购物外出就餐)
F43=调研.用户.车辆行驶路面.Contains(市内道路)
F44=调研.用户.车辆行驶路面.Contains(高速公路)
F47=轿车.cat==微型
F48=轿车.cat=＝小型
F49=轿车.cat=＝紧凑型
F50=轿车.cat=＝中型
F51=轿车.cat=＝中大型
F52=轿车.type＝=SUV
F53=轿车.type＝=MPV

F39=上下文.ua.Contains("...")

{% endhighlight %}
