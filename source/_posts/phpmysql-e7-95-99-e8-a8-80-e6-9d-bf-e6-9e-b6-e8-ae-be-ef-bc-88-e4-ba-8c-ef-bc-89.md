title: PHP+MySQL留言板架设（二）
tags:
  - PHP
  - 原创作品
id: 79
categories:
  - PHP Programming
date: 2009-05-22 19:54:18
---

这周是我们的专周，开始说是今天下午需要把那15页的实验设计图交上去，但今天早上老师看到很多人都没写完，所以将时间延后到星期一，也给我了喘息的时间，今天早上抄了一上午，也才抄了8页而已。

前端时间虽然解决了代码高亮的问题，但是标签智能在HTML的模式下编辑，一旦点击了可视化编辑器，WordPress会自动将HTML标签转义，所以每次只要用到代码高亮，我就得完全在HTML模式下编辑，虽然麻烦，但也是没有办法的办法了。

上次说到留言板的构架，（[PHP+MySQL留言板架设（一）](http://blog.liuyixi.com/index.php/2009-05/61)）其实一个简单的留言板功能已经能够实现，今天说下几个细节方面的注意。

首先是内容是否为空的判断，其实可以发现，如果表单内容为空的话，会引起SQL语言的错误而导致SQL语言不执行，但怎样才能更人性化点呢。
这个时候我们需要加上一个对表单内容的判断函数，当然可以用一段PHP脚本来实现，但是有种更方便的实现方法，那就是通过javascript来实现对表单内容的判断。

首先需要将我们编写的add.php文件中的表单部分加上一个执行标签，以判断通过javascript函数值返回的内容。

[sourcecode language='HTML']<form action="add.php" method="get" name="myform" onsubmit="return CheckPost();">

[/sourcecode]

我们将这个判断函数定义为CheckPost();然后在add.php文件中添加一段javascript的脚本

[sourcecode language='javascript']function CheckPost()
{
	if (myform.user.value=="")
	{
		alert("请填写用户名");  //发出警报
		myform.user.focus();   //将光标聚焦到user表单
		return false;   //返回false值
	}
	if (myform.title.value.length<5)
	{
		alert("标题不能少于5个字符");
		myform.title.focus();
		return false;
	}
	if (myform.content.value=="")
	{
		alert("必须要填写留言内容");
		myform.content.focus();
		return false;
	}
}[/sourcecode]

这个时候每次提交表单的时候都会先经过javascript函数判断，但返回的值为真时，再将表单内容返回到PHP代码中进行执行。

然后是第二个地方，现在的留言板中，是无法输入回车和空格（空格无论多少只显示一个）的，这个时候需要用PHP中的str_replace（）函数将留言框中的空格，回车等转义成HTML能识别的格式。

这个时候在conn.php中添加这段代码
[sourcecode language='php']function htmtocode($content) {
	$content = str_replace("\n", "
", str_replace(" ", "&nbsp;", $content));
	return $content;[/sourcecode]

这断代码的意思是将空格和回车分别替换成HTML能识别的格式。

好了，大概就这样，下次我大概(因为思想漂浮不定）会做关于PHP中cookie的实现例子。

Ps.模板现在也算是大概的完工了，但还有些地方需要细节的修饰，而且我在我的电脑上看到内容于边栏的那个分割线的时候总觉得很怪异，有时虚线都变成了实线了，这个问题究竟是什么原因，还没有找出来，模板完整的完工后，我也给打包起来然后发布O(∩_∩)O哈哈~