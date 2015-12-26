title: 让DIV居网页底端
tags:
  - CSS
  - 技巧
id: 621
categories:
  - DIV+CSS Design
date: 2010-07-15 22:58:01
---

我要将一个图片作为网站的底部，直接在body 的backgroud 中写成bottom 属性显然是达不到我的要求的，因为我的页面在浏览器高度比较高的情况下内容是无法撑满整个浏览器的，所以在body 的background 将图片写成bottom属性在这种情况下面会显示一片空白，像这样：

[![](http://blog.liuyixi.com/wp-content/uploads/2010/07/4.jpg "4")](http://blog.liuyixi.com/wp-content/uploads/2010/07/4.jpg)

很容易看到页面下面是一片空白。
这个时候想到用一个层来让他浮动在底部来放置这张图片，但要适应浏览器高度让层在底部，所以CSS这样写。
<pre lang="CSS" line="1" file="download.txt" colla="+">
#foot{
  width:100%;
  height:500px;
  position:absolute;
  top:100%;
  margin-top:-500px;
  background:url(footer.jpg) center bottom no-repeat;
}
</pre>
刷新页面后，咋一看，好像已经得到了想要的效果：

[![](http://blog.liuyixi.com/wp-content/uploads/2010/07/1.jpg "1")](http://blog.liuyixi.com/wp-content/uploads/2010/07/1.jpg)

<!--more-->

但是，当我们把浏览器的高度降低，出现上下滚动条时，问题就出现了：

[![](http://blog.liuyixi.com/wp-content/uploads/2010/07/2.jpg "2")](http://blog.liuyixi.com/wp-content/uploads/2010/07/2.jpg)

当我们把浏览器往下拖动的时候，下面的部分就变成了空白。

为了解决这个问题，我们要用一种hack的写法：
<pre lang="CSS" line="1" file="download.txt" colla="+">
body {
    font-size: 13px;
    background:#f1f1f1;
    color: #000;
    text-align: left;
    margin: 0;
    padding: 0;
    _height:100%;
    _overflow:hidden;
}
#foot{
    z-index:-1;
    height:500px;
    width:100%;
    position:fixed;
    _position:absolute;
    bottom:0px;
    background:url(footer.jpg) center bottom no-repeat;
}
</pre>
同样将浏览器的高度变低后，这个时候便没有什么问题了。

[![](http://blog.liuyixi.com/wp-content/uploads/2010/07/3.jpg "3")](http://blog.liuyixi.com/wp-content/uploads/2010/07/3.jpg)