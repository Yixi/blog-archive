title: innerHTML 和 creatElement 的区别
tags:
  - DOM
  - javascript
id: 837
categories:
  - javascript
date: 2011-04-15 14:44:31
---

在某些时候，我们需要使用js动态的对DOM进行添加操作。比如我们需要添加一段 &lt;div id="foot"&gt;&lt;/div&gt;，这个时候有两个选择：

第一是使用 innerHTML
<pre lang="javascript" line="1" file="download.txt" colla="+">
document.body.innerHTML+='<div id="foot"></div>';
</pre>
第二种事使用 createElement方法

<pre lang="javascript" line="1" file="download.txt" colla="+">
var newdiv = document.createElement('div');
newdiv.id="foot";
document.body.appendChild(newdiv);
</pre>

两种方法都可以实现，但看起来第一种方法要简单的多，而且如果需要添加的DOM比较发杂，第二种方法会更繁琐。

两种方式的区别在哪里？

第一种方式的原理在把原有的body部分的html取出来加上foot那段DIV，然后再写入body内，所以可能会造成所谓的“闪烁”
而第二种方式是用的对象创建的方法去添加DOM。

而我在Read Later Fast 的content script中像页面添加 page saved/link saved 的 notification是用的第二种方式。而由我接手的Quick Note在页面中添加笔记的插入sidebar的方式我也将在下一版本中换成第二种方式。

之所以这样，是因为之前用第一种方式，重写HTML后，可能会造成页面原有的javascript失效，尤其是那种主要是由javascript构架的站点，而换成第二种方式便不会造成这类问题。

这就是为什么以前版本的Read Later Fast 以及当前还在的Quick Note版本在某些页面使用时会导致当前页面的js工作不正常，比如google reader。

当然比较推荐的办法还是去使用jquery来创建DOM。

用哪种方式，看你测试出来是否有副作用。一般来说 innerHTML只要不是针对body的话，一般都不会存在我提到的这个问题。