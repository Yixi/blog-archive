title: 关于一些jquery
tags:
  - CSS
  - jQuery
id: 594
categories:
  - DIV+CSS Design
date: 2010-04-30 08:57:18
---

这几天终于有心情静下来做一些小的页面。

这学期成了社团的社长，反正还需要在学校待完这学期，所以打算这学期注重于社团文化的建设和社团的管理。

做了一个成员页面，就是一个静态的页面，不过jQuery越写越顺手了。

整个页面的色调取暖色调，是从一款wordpress的主题仿制的。![](http://blog.liuyixi.com/wp-content/uploads/2010/04/AWZ5DAJ9HRNHV1FYQ67.jpg "FORFUN成员")

关于一些jQuery

----

因为为了做左右浮动的效果，为了方便，我是将浮动用jQuery来处理的，但因为有各个不同的层级的内容，所以jQuery不能用最基本的选择器。

第二是全部收起的部分，因为最上面的不需要收起，但都是同样class 的DIV，所以在第一个div中不光有一个class 还多做了个id 用来判断jQuery筛选。像这样：&lt;div class="member" id="ganbu"&gt;   而其他同级的只是 &lt;div class="member"&gt;

这两个部分的jQuery是这样：
<pre lang="jQuery" line="1" file="download.txt" colla="+">
#浮动部分

$(".member  .mem:nth-child(odd)").addClass("left");
$(".member  .mem:nth-child(even)").addClass("right");

#全部收起的选择器

$(".shouqi").click(function(){
       $(".member:not(#ganbu)").slideUp("slow");
    })
</pre>
页面打算用PHP来完善，能个实现管理的功能，以及评论，个人展示之类。