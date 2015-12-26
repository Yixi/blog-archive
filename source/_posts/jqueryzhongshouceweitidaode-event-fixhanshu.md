title: Jquery中手册未提到的$.event.fix函数
tags:
  - jQuery
  - 函数
id: 927
categories:
  - javascript
date: 2011-07-16 17:17:20
---

接手 Diigo chrome extension的项目后，最近一段时间一直都在熟悉这个项目的代码。

之前那位同事在处理事件绑定的时候用到了
<pre lang="Javascript" line="1" file="download.txt" colla="+">
var event = $.event.fix(event || window.event);
</pre>
来处理修正事件。

$.event.fix 这是我以前没有见过的jquery用法，手册中也从未提到这个用法，看这个用法，应该是用来修正事件的。

看了下这段的jquery源码后，大概了解了是这么一个意思。

做前端开发，在调试各个浏览器的童鞋应该知道，各个浏览器对事件处理的方式是不同的，比如说IE下触发事件元素是：event.srcElement，而在firefox下又是 event.target。

而 $.event.fix 的作用就是把浏览器的事件修正为统一的jQuery.Event，这样在不同的浏览器中我们不需要考虑不同的事件触发元素。

当然如果，你如果是通过jquery来绑定DOM的事件，得到的已经是jQuery.Event，就不需要考虑这样的问题。这种一般用在那种写在DOM中的 onclick=""这类当中。