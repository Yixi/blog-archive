title: CSS中自定义标签控制对象
tags:
  - CSS
id: 304
categories:
  - DIV+CSS Design
date: 2009-08-11 18:12:31
---

今天在做外卖网站的细节美化时遇到了一个问题，当我在容器中使用了下面这个属性：

display:block;

此属性能够让每个对象输出后自动换行，例如下面这样的代码：
> &lt;p&gt;位置1&lt;/p&gt;&lt;p&gt;位置2&lt;/p&gt;&lt;p&gt;位置3&lt;/p&gt;
显示后的结果如下面：

位置1

位置2

位置3

这个时候如果我们想控制其中对象的颜色就比较麻烦，比如我想让“位置”两个字为黑色，里面的数字为红色。

当然可以写上font标签实现，或者用新的层属性来定义，但如果用新的层话会再次发生换行。

这个时候可以用自定义的标签来简单实现

我们将代码改为：

&lt;p&gt;位置&lt;c&gt;1&lt;/c&gt;&lt;/p&gt;&lt;p&gt;位置&lt;c&gt;2&lt;/c&gt;&lt;/p&gt;&lt;p&gt;位置&lt;c&gt;3&lt;/c&gt;&lt;/p&gt;

然后在CSS文件中定义：

c{
color:red;
}

便可以简单的实现。