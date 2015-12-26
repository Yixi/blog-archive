title: 用CSS3绘制的Diigo图标
tags:
  - css3
  - diigo
id: 912
categories:
  - DIV+CSS Design
  - 工作记录
date: 2011-07-08 15:23:57
---

最终效果如图：

[![](http://blog.liuyixi.com/wp-content/uploads/2011/07/css3diigo1.png "css3diigo")](http://blog.liuyixi.com/wp-content/uploads/2011/07/css3diigo1.png)

diigo的icon比较简单，分析后一个环形+一条竖线。

绘制原理：

通过设置border-radius的值为正方形div的一半来绘制原型，以及使用background线性渐变来绘制背景。

具体实现代码如下：

<pre lang="css" line="1" file="download.txt" colla="+">
<!-- HTML-->
<div class="back">
        <div class="wai"></div>
        <div class="nei"></div>
        <div class="shu"></div>
</div>

<!-- Css -->
<style>
    .back{
        width:100px;
        height:100px;
        background:-webkit-gradient(linear, left top, left bottom, from(rgb(84,185,255)), to(rgb(0,79,180)));
        background:-moz-linear-gradient( top, rgb(84,185,255), rgb(0,79,180));
        border-radius:10px;
        border:1px solid rgb(87,163,221);
        -webkit-box-shadow:inset 0 0 5px rgba(255, 255, 255,1);
        -moz-box-shadow:inset 0 0 5px rgba(255, 255, 255,1);
        position:relative;
    }
    .wai{
        width:64px;
        height:64px;
        background:#fff;
        position:absolute;
        left:18px;
        top:22px;
        border-radius:32px;
    }
    .nei{
        width:44px;
        height:44px;
        background:-webkit-gradient(linear, left top, left bottom, from(rgb(84,185,255)), to(rgb(0,79,180)));
        background:-moz-linear-gradient( top, rgb(84,185,255), rgb(0,79,180));
        border-radius:22px;
        position:absolute;
        left:28px;
        top:32px;
    }

    .shu{
        width:10px;
        height:54px;
        background:#fff;
        left:72px;
        top:0px;
        position:absolute;
    }  
</style>
</pre>

[你也可以使用一个支持CSS3的浏览器点击这里查看demo](http://lab.liuyixi.com/pages/diigoiconbycss3.html)

下次有空试试绘制右边栏那个完整的Diigo Logo