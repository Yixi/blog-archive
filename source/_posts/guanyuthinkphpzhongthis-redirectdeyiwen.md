title: '关于ThinkPHP中$this->redirect的疑问。'
tags:
  - ThinkPHP
  - 函数
  - 开发
id: 465
categories:
  - PHP Programming
date: 2009-12-30 16:49:21
---

在TP1.5版本中使用

<pre lang="PHP" line="1" file="download.txt" colla="+">
$this->redirect('login','Public');
</pre>
便可以实现跳转到当前项目的 PublicAction 中的 login 方法路径。

在TP2.0中方法发生了变动，按手册上的方法应该这样进行跳转:
<pre lang="PHP" line="1" file="download.txt" colla="+">
$this->redirect('Public/login');
</pre>

但是最后的URL地址却会变成：

> http://xxx.xxx.xxx/admin.php/Admin_App//Public/login

但我实际需要跳转的地址是

> http://xxx.xxx.xxx/admin.php/Public/login

也就说，默认的$this->redirect方法会在url中加上项目名。有人建议说重写一下TP中的redirect方法，这比较麻烦了。

这时想到了用redirect()函数，而不使用$this中的方法，然后想到了两个解决办法:
<pre lang="PHP" line="1" file="download.txt" colla="+">
$this->redirect('../../Public/login');  //方法1

redirect('admin.php/Public/login')   //方法2
</pre>

其中第一个办法虽然能解决，但因为路径层数比较复杂，而我也一直比较避免用 ../到url路径中。

第二个办法虽然能解决，但是并不是完善，因为在设计中我考虑到以后可以任意的改变 admin.php这个后台入口文件的文件名。

尝试了redirect()函数中并不能使用TP自带的替换变量后，突然想到加一个变量赋值的笨办法:
<pre lang="PHP" line="1" file="download.txt" colla="+">
 $login_url = __APP__.'/Public/login';   //跳转路径
 redirect($login_url);
</pre>

这样就算把问题解决了。

TP中不少的函数和模板替换值 比如之前遇到的 ../Publc  都会自动加上项目名称，当时本来项目名想作为title的一个替换量，但在使用 ../Publc 时路径会变成 http://xxx.xxx.xxx/项目名/Tpl/Public/ 所以当时不得不把项目名换成了和文件目录名相同。

这点我觉得完全没必要了。 