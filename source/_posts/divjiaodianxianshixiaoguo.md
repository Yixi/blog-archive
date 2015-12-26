title: DIV焦点显示效果
tags:
  - 折腾
  - 探索
id: 712
categories:
  - DIV+CSS Design
date: 2010-10-08 16:59:33
---

今天看到一个jQuery的图片焦点显示放大显示效果，心血来潮想着用CSS来实现。

下面是尝试过程。

首先用5个层平铺做为备用，因为要居中显示，所以用到了display:inline-block属性。而如果使用float:left的话，所有元素向左浮动，在hover事件元素变宽时会只向右边延展，效果不好。

这个时候开始分析，在元素的hover CSS中变化宽度和高度，以及颜色。

[![](http://blog.liuyixi.com/wp-content/uploads/2010/10/1.jpg "1")](http://blog.liuyixi.com/wp-content/uploads/2010/10/1.jpg)

[点击查看doem](http://blog.liuyixi.com/upload/20108101.html) （在chrome下浏览）
<!--more-->

下面是CSS：
<pre lang="css" line="1" file="download.txt" colla="+">
<style>
        #test{
            width:600px;
            height:100px;
            border:1px solid #ff0000;
            margin:100px auto;
            overflow:hidden;
            text-align:center;
            padding:50px 0;
        }
        .a{
            width:70px;
            height:100px;
            background:green;
            display:inline-block;
        }
        .a:hover{
            background:blue;
            width:80px;
            height:110px;
        }
    </style>
</head>
<body>
    <div id="test">
        <div class="a"></div>
        <div class="a"></div>
        <div class="a"></div>
        <div class="a"></div>
        <div class="a"></div>
    </div>
</body>
</pre>

这时候鼠标移动到层上有了宽度和高度的变化，但是由于inline的基准线，底部高度一样，这个时候尝试将hover中的外补丁加上负边距。问题解决。

[![](http://blog.liuyixi.com/wp-content/uploads/2010/10/2.jpg "2")](http://blog.liuyixi.com/wp-content/uploads/2010/10/2.jpg)

[点击查看doem](http://blog.liuyixi.com/upload/20108102.html) （在chrome下打开）

下面是CSS

<pre lang="css" line="1" file="download.txt" colla="+">
    <style>
    *{
        margin:0;
        padding:0;
        outline:0;
    }
        #test{
            width:600px;
            height:200px;
            border:1px solid #ff0000;
            margin:100px auto;
            overflow:hidden;
            text-align:center;
            padding:50px 0;
            letter-spaceing:-4px; font-size:0;
        }
        .a{
            width:100px;
            height:200px;
            background:#D1D1D1;
            display:inline-block;
            letter-spaceing:0; font-size:size;
            -webkit-box-shadow:0px 0px 10px #d1d1d1;
        }
        .a:hover{
            background:#A2C838;
            width:140px;
            height:220px;
            margin:-10px 0;
            -webkit-box-shadow:0px 0px 10px #A2C838;
        }
    </style>
</head>
<body>
    <div id="test">
        <div class="a"></div>
        <div class="a"></div>
        <div class="a"></div>
        <div class="a"></div>
        <div class="a"></div>
    </div>
</body>
</pre>

这个将效果做了一些优化，但尝试在层中写内容后，效果会变得和最上面一样，所以还不完善。

等继续完善。