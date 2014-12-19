---
layout: news_item
title: 'Mac+Github Pages+Jekyll配置个人网站'
author: AcePeak
categories: [Mac Github Jekyll Internet Website Domain]
---

`1 Github官网注册账号`

[Github.com官网](https://github.com/)


`2 下载Github For Mac并登录`

[Mac版Github下载页面](https://mac.github.com/)


`3 设置Git方式同步并使用SSH Keys`

[前往此贴查看changsj的回答](http://segmentfault.com/q/1010000002169878)

`4 使用Jekyll`

[首先更换GEM源](http://www.365dw.cn/616.html)

[按照Jekyll首页所列的代码指令开始吧](http://jekyllrb.com/)


`5 从Jekyll建立主页`

[Fork Jekyll并clone到桌面吧](https://github.com/jekyll/jekyll)

[创建Pages代码库](https://pages.github.com/)

然后通过Github For Mac将<username>.github.io和jekyll代码库下载到你的电脑上，把Jekyll代码库中的sites文件夹内所有文件拷贝到<username>.github.io代码库根目录下


`6 绑定域名`

[官方绑定攻略](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/)

要(很)注(坑)意(爹)的是，在[绑定根域名][*bind-domain*]时, 网页上列出的两个IP地址(192.30.252.XXX)都不是你的IP，你需要在命令行知道你自己的http://<username>.github.io的IP是多少，ping之吧。


`7 编写网站吧`

[Jekyll官方文档](http://jekyllrb.com/docs/home/)

`8 提交网站`

由于在Jekyll体系中，_site文件夹是本地服务器Jekyll生成最终html的地方，.sass-cache文件夹是本地的sass缓存文件，都不需要作为代码文件上传到服务器上，因此可以在Github For Mac中设置ignored files为

{% highlight PowerShell %}
_site/
.sass-cache/
{% endhighlight %}


`9 Enjoy(Painful)!`

[*bind-domain*]: https://help.github.com/articles/tips-for-configuring-an-a-record-with-your-dns-provider/