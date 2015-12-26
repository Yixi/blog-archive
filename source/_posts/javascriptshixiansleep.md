title: Javascript实现sleep
tags:
  - javascript
  - 技巧
id: 1107
categories:
  - javascript
date: 2013-03-02 00:36:02
---

js中没有sleep等待的方法，但是有一个方法可以实现同步的sleep，而不需要用settimeout的回调实现。

代码如下：

<pre lang="Javascript" line="1" file="download.txt" colla="+">

function sleep(milliSeconds){
   var startTime = new Date().getTime();
   while (new Date().getTime() < startTime + milliSeconds);
}

//use

sleep(10000);

</pre>