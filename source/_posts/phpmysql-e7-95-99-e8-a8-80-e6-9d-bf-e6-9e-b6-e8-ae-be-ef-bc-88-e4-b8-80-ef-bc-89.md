title: PHP+MySQL留言板架设（一）
tags:
  - PHP
  - 原创作品
id: 61
categories:
  - PHP Programming
date: 2009-05-20 22:03:29
---

昨天博客的访问恢复后，就一直去寻找WordPress的语法高亮插件，瞎折腾半天，语法高亮问题仍然没解决，coolcode在判断HTML的<>标记语言时会发生错误.
事情是这样，因为一个高中的女同学（汗···）一直吵着闹着要和我学做网站，我问她要学简单的还是厉害的，她说要学习厉害的，我说那好吧，现在比较流行PHP开发，那你去学PHP吧，她果真就去了，现在应她的要求，所以现在在博客上会做一系列的PHP实例程序出来。

言归正传，她语法也看的差不多了，今天就做一个小的总结，做一个简单的留言板程序的实现。

首先是整体的文件规划图：
[caption id="attachment_38" align="alignnone" width="300" caption="文件规划图"]![文件规划图](http://blog.liuyixi.com/wp-content/uploads/2009/05/e79599e8a880e69dbfe7a88be5ba8f-300x114.jpg "文件规划")[/caption]

在架构程序之前，首先需要在数据库中新建一个表。将下面的语言复制到phpmyadmin中或者其他数据库管理软件中执行：

[sourcecode language='sql']CREATE TABLE `message` (
  `id` tinyint(1) NOT NULL auto_increment,
  `user` varchar(25) NOT NULL,
  `title` varchar(50) NOT NULL,
  `content` tinytext NOT NULL,
  `lastdate` date NOT NULL,
  PRIMARY KEY  (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=gbk AUTO_INCREMENT=1 ;[/sourcecode]

或者你可以在phpmyadmin中手动建表。

然后首先是第一个文件的编写，第一个文件首先是数据库配置文件(conn.php):

[sourcecode language='php']<?php
  $conn = mysql_connect("localhost","root","root") or die("连接数据库失败");
  mysql_select_db("testd",$conn) or die("打开数据库失败");
  mysql_query("set names 'GBK")
 ?>[/sourcecode]

数据库配置文件编写好过后，然后就是留言板添加文件(add.php)的编写：

[sourcecode language='php']<?php
include 'conn.php';
  if ($_GET['submit']){

  	 $sql="INSERT into message (id,user,title,content,lastdate)".
  	             "values (NULL,$_GET[user],$_GET[title],$_GET[content],now())";

  	$panduan=mysql_query($sql);
  	if ($panduan){
  		echo "成功";
  	}else echo"失败,SQL:$sql
:错误
".mysql_error();
  }
?>

<form action="add.php" method="GET">
用户:<input type="text" size="10" name="user"/>

标题:<input type="text" size="20" name="title"/>

内容:<textarea name="content"></textarea>

<input type="submit" name="submit" value="Ok"/>
</form>[/sourcecode]

最后是列表文件(List.php)的编写
[sourcecode language='php']<?php
include 'conn.php';
?>

<table width=500 border="0" align="center" cellpadding="5" cellspacing="1" bgcolor="#add3ef">

<?php
 $sql="SELECT * FROM message order by id desc";
 $query=mysql_query($sql);
 while ($row=mysql_fetch_array($query)){
?>

  <tr bgcolor="#eff3ff">
  <td>标题：<?=$row[title] ?> 用户：<?=$row[user] ?> 留言日期：<?=$row[lastdate] ?></td>
  </tr>
  <tr bgColor="#ffffff">
  <td>内容：<?=$row[content] ?></td>
  </tr>

  <?php
 }
   ?>

</table>[/sourcecode]

还有更多的下次将会完善，比如留言删除，修改等功能的实现，其实如果细心，将会知道，其实也就是数据库的操作方法。

因为代码高亮插件有点问题，不能正常判断HTML标签的位置，所以放弃了用代码高亮，请谅解，可能语法有些分号漏掉，请注意查明。具体的语法结构下次来讲解且完善，被那个代码高亮的问题搞的太累了，一直在寻找解决办法