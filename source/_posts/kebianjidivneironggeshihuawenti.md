title: 可编辑DIV内容格式化问题
tags:
  - contenteditable
  - pre
  - readablility
id: 1068
categories:
  - HTML5
  - javascript
date: 2012-09-16 11:33:16
---

contenteditable 的 div 内容标签格式化问题，以前在做quick note的时候都有遇到过，因为会遇到从网页中拷贝内容进去，或者拖拽内容进去。在这种情况下，在div的编辑区域会保留原页面内容的DOM结构以及样式，即使从其他地方复制一个纯文本内容也会产生一个inline的div标签。

之前在quick note中为了保证内容是纯文本的text，在每次内容变动时都会使用一个函数来去掉内容中多余的标签。当时借鉴了readability中的一个算法，通过递归来逐层去掉内容中的标签。但这个算法在处理过大的内容时，明显会有较长的时间延迟，并不是一个最佳的方案。

最近在研究一个新的项目时，遇到同样的问题。想到以前的quick note中的问题，想重新找一种方案来实现文字的clean处理，以前是找出element标签来通过正则去掉标签，效率自然低下。是否可以尝试通过递归将div中的textNode内容提取出来再处理呢？

简单尝试了下，确实可行，但文字按照原顺序重组的却遇到了问题，特别在那种块级标签包含行级标签的内容中（应该是我想的还不够透彻，所以暂时没有管这个问题）。

这时候却让我突然想起了&lt;pre&gt;标签。

&lt;pre&gt;标签中的内容是预格式化的文本标签。

当把内容放进去过后，让我很是高兴，无论拷贝什么内容进去，最后保留下来的便是纯粹的text内容。根据这一特性，写出了一个新的处理clean内容的办法。

&nbsp;

<pre lang="javascript" line="1" file="download.txt" colla="+">

//base on Jquery;
//use  var clearn = $(this).getPreText();

$.fn.getPreText = function () {
    var text = $("<pre />").html(this.html());
    if ($.browser.webkit)
        text.find("div").replaceWith(function () { return "\n" + this.innerHTML; });
    if ($.browser.msie)
        text.find("p").replaceWith(function () { return this.innerHTML + "
"; });
    if ($.browser.mozilla || $.browser.opera || $.browser.msie)
        text.find("br").replaceWith("\n");
    return text.text();
};

</pre>

DIV中可能会产生标签的情况是可以列举出来的，我们只需要控制固定的来源就行了。比如这个方法我们可以监听到ctrl+v时间时再来执行。
当然，还有其他很多种来源都会产生标签的，比如回车，会产生一个新的div，等等。如果需要保证内容纯文本，还需要监听各种来源情况，这是后话，以后再谈。