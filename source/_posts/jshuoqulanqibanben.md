title: JS 获取浏览器版本
tags:
  - chrome
  - firefox
  - IE
id: 989
categories:
  - javascript
date: 2011-10-11 17:06:54
---

在写JS时，很多情况我们需要知道浏览器的版本来做一些工作。

javascript获取浏览器版本方法：

<pre lang="Javascript" line="1" file="download.txt" colla="+">
//获取浏览器名
navigator.appName    // Microsoft Internet Explorer / Netscape 等等

//针对IE 获取详细浏览器版本
navigator.appVersion.split(";")[1]   // MSIE 8.0 / 7.0 /6.0

//其他获得浏览器详细版本
navigator.appVersion 
</pre>

在chrome/firefox中，navigator 这个全局对象还提供了更多的关于客户端的信息，有兴趣可以console一下或者each一下。