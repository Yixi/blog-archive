title: 贴一段数列菜单CSS样式。
tags:
  - CSS
id: 335
categories:
  - DIV+CSS Design
date: 2009-09-02 21:53:32
---

这几天在做一个报名系统的时候，写到后台菜单栏时调整后的一种样式，颜色搭配是他们后来建议我进行修改的。

这几天对于导航条和菜单栏制作想到了很多的方法，待我整理好代码后将会一一放出，并做出专门的演示页面进行演示。

刚开学，这段时间有很多的事情需要忙，筹划很久的项目也要正式的退出了，如果细心的人可能已经发现我博客的“我管理的网站”里面多添加上了两个链接，但是里面一个没有内容，而另一个的内容还在完善之中。

关于这个，暂时不作过多的说明。

内容将会逐渐的添加上去。

下面是竖形菜单栏的CSS样式之一，至于用法，不需要多说了吧，如果实在不知道，在评论中回复吧。
<pre lang="css" line="1" file="download.txt" colla="+">
#menu li{
	border-bottom:1px solid #ed9f9f;
}
#menu li a{
	display:block;
	padding:5px 5px 5px 1.5em;
	text-decoration:none;
	border-left:12px solid #711515;
	border-right:1px solid #711515;
}
#menu li a:link, #menu li a:visited{
	background-color:#c11136;
	color:#ffffff;
}
#menu li a:hover{
	background-color:#990020;
	color:#ffff00;
}
</pre>