title: CSS中background处理图片的技巧
tags:
  - CSS
id: 152
categories:
  - DIV+CSS Design
date: 2009-05-31 14:03:22
---

常规在许多的页面中少不了图片的装饰，最常见的比如是内容容器的标题部分：

[caption id="attachment_153" align="alignnone" width="242" caption="simple"]![simple](http://blog.liuyixi.com/wp-content/uploads/2009/05/e5ae9ee4be8b.jpg "simple")[/caption]

 如上面页面的公告部分，在上面的小表格中平铺了一层背景，当我们需要在页面中呈现不同颜色的标题栏的时候，我们只需再建一个不同颜色的图片文件，比如Image1，image2，image3，image4···

是不是嫌图片多了管理起来麻烦呢？其实这个时候我们可以很好的利用CSS 中的background操作图片的属性。

 我们来先看一张图片：

[caption id="attachment_154" align="alignnone" width="300" caption="bordercolored"]![bordercolored](http://blog.liuyixi.com/wp-content/uploads/2009/05/bordercolored-300x63.jpg "bordercolored")[/caption]

<div class="mceTemp"> </div>
<div class="mceTemp">上面的图片中包含了7种颜色的标题背景，我们可以根据自己的需要取出自己需要的部分即可，这个该怎么实现呢？</div>
<div class="mceTemp"> </div>
<div class="mceTemp">这个时候我们可以通过CSS中的background属性来实现，我们假设每个标题颜色的高度为 20px，那么我要取第5条红色的标题栏可以这样实现：</div>
[sourcecode language='css'].style{height:20px;background:url(table.gif) no-repeat 0px -80px;}[/sourcecode]

其中在url图片后面的参数 0px  -80px的意思便是从横坐标0px处，纵坐标80px处开始取我们规定的高度20px的图片，同理，我们只需要修改后面的两个像素参数便可以取出我们想要的部分了。

利用这个属性，我们不光可以实现图片的统一化管理，还有更好的用处。比如下面的那样的标题栏

[caption id="attachment_155" align="alignnone" width="241" caption="simple2"]![simple2](http://blog.liuyixi.com/wp-content/uploads/2009/05/212.jpg "simple2")[/caption]

<div class="mceTemp">留意其中我圈出的部分，那个是圆滑过渡的标题栏部分，要实现这样的效果可以做一个和表格同宽度的图片后作为表格的背景便可以，但如果增宽宽度的话，那么我就需要做一个新的图片对应新宽度，以实现两边圆滑的效果：</div>
<div class="mceTemp"> </div>

[caption id="attachment_156" align="alignnone" width="423" caption="长标题栏"]![长标题栏](http://blog.liuyixi.com/wp-content/uploads/2009/05/e995bfe5baa6e58f98e58c96.jpg "长标题")[/caption]

遇到这样的标题栏的时候，我们就需要重新做一个适应这个宽度的图片。

其实就像最上面讲的那样，我们当然可以将不同宽度的图片做到一张图片里面，像这样：

[caption id="attachment_158" align="alignnone" width="185" caption="不同宽度图片"]![不同宽度图片](http://blog.liuyixi.com/wp-content/uploads/2009/05/e7bb9fe4b880.jpg "不同宽度图片")[/caption]

不同宽度图片利用最上面讲的原理进行不同部分图片的取舍，其实仔细会发现，我们在最上面的部分只是定义了纵坐标的位置取定，利用同样的方法，为什么我不可以再横坐标上取我们想要的部分呢？

像那不同的标题宽度的图片，我们可以做成一张整体的长图，像这样：
<div class="mceTemp"><dl id="attachment_160" class="wp-caption alignnone" style="width: 173px;"><dt class="wp-caption-dt">![长](http://blog.liuyixi.com/wp-content/uploads/2009/05/e995bf1.jpg "长")</dt><dd class="wp-caption-dd">长</dd></dl>假设我们这张为chang.gif的图片的宽度为300px，而需要我们去适应的标题栏的宽度分别为100px和200px。</div>
<div class="mceTemp"> </div>
<div class="mceTemp">按照原理，在适应100px宽度的标题栏时我们可以先取出宽为80px 然后再取出整体chang.gif的最右20px作为拼接。</div>
<div class="mceTemp">同理，200px的标题栏，我们可以先取出180px宽度，然后再用最右的20px进行拼接。</div>
<div class="mceTemp"> </div>
<div class="mceTemp">整体代码可以如此实现：</div>
<div class="mceTemp"> </div>
<div class="mceTemp"> </div>
首先是CSS样式文件：
[sourcecode language='css']
.style1 h1{width:80px;background:url(chang.gif) no-repeat 0px 0px;}
.style1 span{width:20px;background:url(chang.gif) no-repeat -280px 0px;}
.style2 h1{width:180px;backgound:url(chang.gif) no-repeat 0px 0px;}
.style2 span{width:20px;background:url(chang.gif) no-repeat -280px 0px;}
[/sourcecode]

在调用时，我们这样调用:
[sourcecode language="HTML"]
<div class="style1">

# 这是100px宽度的标题栏<h1><span></span>
</div>
<div class="style2">
<h1>这是200px宽度的标题栏
<span></span>
</div>
[/sourcecode]

是不是感到很方便的就实现了不同宽度的标题栏调用一个文件实现了呢？

CSS可以说是网页设计中的魔术棒，利用好了这魔术棒，将会为你的网页添置不一样的色彩。