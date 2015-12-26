title: 这下郁闷了
tags:
  - jetpack
id: 894
categories:
  - Firefox
date: 2011-06-21 15:36:23
---

因为quick note for firefox在外面的版本不兼容firefox5，是因为使用1.04b版本的add-on SDK build的，而使用1.05b版本就可以与firefox5兼容，但由于1.05b版本中有个jetpack确定的插件reload机制的BUG，所以暂时没有采用。

而最近收到邮件说jetpack 1.0 准备正式发布，去网站上下载回来后，测试发现个很大的问题，原先的pageMod不能向resouce://打头的页面插入contentscript，而这个的结果便是导致我们目前的所有awesome screenshot ,quick note,read later fast 的firefox版本功能完全失效。

目前还不知道是因为安全原因jetpack这样做还是因为BUG的原因