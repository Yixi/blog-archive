title: DIV横向排列平铺。
tags:
  - CSS
  - DIV
  - 技巧
id: 374
categories:
  - DIV+CSS Design
date: 2009-10-07 19:32:32
---

![Div横向平铺](http://blog.liuyixi.com/wp-content/uploads/2009/10/divhenxiang.jpg "Div横向平铺")

先上图。

所谓横向的平铺就像上面那样的内容模型那样，首先是一个容器，也就是途中的半透明的部分，然后里面的内容用类似矩形的形状进行平铺，内容由PHP脚本的循环进行输出。

其实在之前的外卖网站制作的过程中就考虑的是这样的布局方式，只是当时对这种方式模型理解的不够透彻，所以在布局中存在一定的bug，虽然用其他的办法进行弥补和掩饰，但问题始终是问题，是依然存在的。

这次的布局中，思路比较清晰，所以理解上比之前的布局要透彻一些。

<!--more-->

好了 废话不多说，上代码。我贴上图片中间半透明部分的所有源码
<pre lang="HTML">
<div class="boxlist">
<div class="boxlisttop">
			         {dede:list col='1' row='3' titlelen='20' infolen='100' imgwidth='120' imgheight='80' pagesize='18' typeid='95'}
<div class="smallbox">
<div class="imagebox">[field:imglink/]</div>
<div class="textlink">[field:textlink/]</div>
</div>
{/dede:list}</div>
<div class="boxlistbottom">   {dede:pagelist listitem="info,index,end,pre,next,pageno" listsize="5"/}</div>
<div class="list_copyright">
		            {dede:global.cfg_powerby/} 建议在IE7以上，且在1280*800分辨率下浏览</div>
</div></pre>
<pre lang="CSS">/*CSS部分*/
.boxlist{
  position:absolute;
  width:900px;
  height:440px;
  background:url(boxbg.png);
  top:35px;
  left:30px;
  padding:20px 0 20px 0;
}
.boxlisttop{
   height:360px;

}
.boxlistbottom{
   padding:10px 0 0 0;
   text-align:center;
}
.smallbox{
	float:left;

  width:150px;
  height:120px;
}

.imagebox{
   width:120px;
   height:80px;
   margin:0 auto;
   border:1px solid #b3b3b3;
}
.textlink{
  text-align:center;
  padding:7px 0 0 0;
}

.list_copyright{
	position:absolute;
	height:20px;
	width:900px;
	bottom:0px;
	left:0px;
	text-align:center;
	color:#fff;
}</pre>