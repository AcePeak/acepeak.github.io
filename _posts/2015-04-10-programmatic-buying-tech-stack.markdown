---
layout: blogs_item
title: 【深挖】品牌程序化购买具体细节Programmatic Buying tech stack
author: AcePeak
categories: [广告平台]
tags: 
- 市场
---


##1. Adserving 第三方广告伺服


最近经常有专业人士问，互联网广告为何需要要adserving？adserving在中国以前都是由publisher或者adnetwork免费提供的，它是一种广告弹射方式，也是一种承载带宽的高阶tracking，为何广告主要为Doubleclick，Sizmek，秒针，筷子科技的adserving支付额外费用（预算的2%-15%根据素材尺寸大小)，而不用免费的呢？adserving能提供的report，普通监测也能提供，为何需要有这么一环adserving在广告生态中？在国外还衍生出这么多上市企业？


这个问题确实比较难回答，首先小编先植入读者一个概念叫做“需方控制权，“demand side control power”。


可以这么说，现如今中国的数字品牌广告Campaign从投放的一瞬间开始，需方控制权基本上就丧失了，广告主或者agency，Campaign中只能拿着第三方监测公司的tracking report去做一些事后诸葛亮的事，补些流量啥的。


Tracking技术在创意，策略，效果根本没法实时优化，所以现在Agency都在努力为广告主争取adserving环境。其实就是为广告主在争需方控制权。


而adserving的环境就能够在四个维度（设计、投放、管理、统计）上进行任意调整，达到需方控制的总目的。任何维度的调整都可以是程序化的，做到透明并且可控。 值得注意的是在这里，adnetwork，dsp与publisher只是投放渠道，需方控制必须在需方，而不是在利益冲突方。 当然这里说的是百万RMB以上预算所应有的需方控制权。值得一提的是，用了Adserving 就不用ad tracking了，因为report与控制权都在需方了。


以下是小编采访Sizmek 副总裁关于adserving的对话很说明问题


Mark Kalus：Adserving 是欧美广告数字投放的标配，Adserving存在的目的主要两个：


第一简化广告主与发布商的之间的流程并扮演第三方的角色，不能小看第三方的作用，任何买卖都需要第三方，实际上我们解决的是诚信与费用交割问题，广告主的支付往往在我们的报表之后。如果广告主的常规预算在10万-20万美金左右，可能不会考虑用国际级的第三方Adserving供应商，但是如果预算是100万美元-200万美元往上的级别，第三方是必须有的。


第二在Adserving基础之上，我们又可以做富媒体，动态创意展示，甚至获得广告主需要的Campaign洞察。数据的获取是一方面，数字广告战役的成功的最重要方面则是Adserving，创意优化还有富媒体的配合。根据comScore的调研，一次成功的数字广告战役，创意的呈现4倍重要于媒体的排期安排。创意占广告成功的52%权重，而媒体排期只有13%.


##2：BrandSafety 品牌安全


BrandSafety有事前与事后，有了Adserving广告的需方控制权，需方就能做到事前BrandSafety，由品牌保护科技公司保护广告主的品牌资产，这里品牌保护公司需要有iframe嵌套穿透 与广告位分级技术。传统数字广告投放充满不符合品牌策略的投放，用了程序化购买反而更能做到BrandSafety。


##3：Viewability 可见曝光


怎么衡量Viewability呢？根据IAB目前的调研，publisher必须遵循Safeframe，才能实现viewability的测量，所以这里需要协会大力推进safeframe的代码布置方式，并且测量机构提Viewability测量的时候必须提有没有对应的safeframe环境。


##4. Brand Performance  品牌效果


要实现viewability测量环境，产业链估计还要等一两年，没有了Viewability广告主怎么衡量品牌效果呢？ 欧美提供了一些结算方式，当然也是基于adserving的。


engagement rate  （消费者与广告互动的率， 点击，玩耍，回答问题） 欧美Tremo,tubemogul 等上市视频效果广告公司甚至根据engagement来结账，一次engagement  2美元。


dwelling rate （鼠标移到广告里的时长率）


IGRP （根据第三方数据来算抵达率）


回搜率 （由搜索引擎提供的归因分析）


##5. Brand Lift  品牌意向


到底消费者有没有购买意向呢？Brandlift 到底有没有？


尼尔森收购了一家公司叫Vizu，它的主要目的是将问卷调查混入广告创意与媒体投放，取控制sampling 与曝光sampling 两个用户群，看曝光sampling与控制sampling的态度变化对比，实时做调查，实时调整广告。


比如你会看到广告创意： 你最近看到肯德基广告了吗？你觉得肯德基是负责任的企业吗？其实都是调查。


##Demand Side Brand exchange（programmatic direct buy）： 需方品牌交换市场,程序化直接购买

宝洁的鹰眼，GroupM 目前都在海内外搭建 Demand Side Brand exchange， 说的是同集团广告需求一旦多样化了，就可以通过母集团采购独有的流量，在创造了adserving环境的情况下，在集团内部做优化，给不同的品牌做曝光优化。 有点像以前的adnetwork 但adserving ，BrandSafety等是第三方的。集团只做采购层面的exchange。