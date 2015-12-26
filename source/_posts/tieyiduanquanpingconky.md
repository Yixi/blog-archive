title: 贴一段全屏conky。
tags:
  - conky
  - Linux
id: 357
categories:
  - 窗外的世界
date: 2009-09-23 22:31:30
---

先上图。

![thedesktop](http://blog.liuyixi.com/wp-content/uploads/2009/09/thedes.jpg "thedesktop")

这个主要是利用了${voffset}和${offset}来控制参数的定位，然后结合背景图片的使用，将桌面改装成这样。

简单介绍下各部分所指的内容，中间为背景图的计算机模型，引出线指向各个部分的参数，不要被计算机模型图忽悠了，那个是背景图片。左边是系统各参数的监控，右边上面为进程前10CPU占用的进程排行，右边中间为ARCH　Linux 的RSS订阅。左边下面分别你是网络进入和网络出去的监控，右下角是一个终端，是tilda软件，依附在桌面，作为桌面的一部分。
如果图片看不清楚的话，[点击这里可以查看大图](http://blog.liuyixi.com/upload/thedes.jpg)

因为conky太长，我将conky配置脚本和背景图片打包在下面

===========================================

[http://blog.liuyixi.com/upload/conky.tar.gz](http://blog.liuyixi.com/upload/conky.tar.gz)

===========================================