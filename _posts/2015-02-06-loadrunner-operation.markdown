---
layout: blogs_item
title: LoadRunner实战系列（二）之流程篇
author: AcePeak
categories:
  - 积累
tags:
  - 原创
  - Web
  - 测试
  - LoadRunner
---


##流程篇


首先打开Virtual User Generator（VuGen）；

创建新Virtual User，选择Web(HTTP/HTML)，点击创建；

弹出了配置框，在里面选择如下内容：

> Application Type: Internet Applications
>
> Program to record: 这里如果有IE8及以下最好，因为LR不支持IE10以上；或者选择Firefox，因为LR对其他浏览器支持也不好。因此这里对我而言，选择firefox程序的所在
>
> URL Address: 选择你需要测试的网址，比如http://www.baidu.com/?q=mobile
>
> Working Directory: 不变即可
>
> Record to Action: 选择Action即可

点击确定后将会进行后台录制，时间很长。对我而言点击取消，直接进入Action代码中进行编码。

结束后将会进入Action代码页中，如果没有代码只有return 0，则可以手动添加你需要的逻辑，常用的有web_url，具体可以参考实战系列（三）之脚本篇

脚本书写完毕后，可以点击Tools->Create Controller Scenario，选择保存脚本后出现创建场景（Scenario）窗口，Vusers选择1000，点击确认进入Controller程序中


进入Controller

在左下角找到Global Schedule窗口，双击Start Vusers，选择开始即同步开启1000VUser，确认

双击Duration，选择30分钟测试，确认；

双击Stop VUsers，选择Stop All Vusers Simulatenously，确认

选择Scenario->Start开始运行，然后就可以观察到各种报表和系统实际承载能力了；
