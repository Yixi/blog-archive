title: 主题第三次修改，响应式设计
tags:
  - 博客
  - 响应式设计
id: 1099
categories:
  - Browser
  - 网络琐事
date: 2013-01-21 22:53:41
---

[![simple gray3](http://blog.liuyixi.com/wp-content/uploads/2013/01/9D75C1CE-5555-419B-B9C2-16E3AA05122B.jpg)](http://blog.liuyixi.com/2013/01/21/zhutidisancixiugaixiangyingshisheji/9d75c1ce-5555-419b-b9c2-16e3aa05122b/)

&nbsp;

昨天晚上花了几个小时时间把博客主题做了一些改动，整体设计改动不大，主要在原主题的基础上添加了响应式支持。

有兴趣的可以用iPhone和iPad分别横向和竖向查看网站。

为了更好的支持响应式设计，将原来的CSS文件完全重写，所以可能有一些细节地方的CSS并没写到可能变现很诡异。

主题内容并没有采用液态内容的方式来支持响应，而是计算了11栏的栅格来做各种宽度的基本框架。因以前文章中的图片img标签中都写死了width 和 height，所以用js删除掉了图片的width 和 height 属性来支持液态图片。

&nbsp;