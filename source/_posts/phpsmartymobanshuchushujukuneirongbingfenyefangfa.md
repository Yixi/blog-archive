title: PHP Smarty 模板输出数据库内容并分页方法。
tags:
  - PHP
  - Smarty
  - 模板
id: 327
categories:
  - PHP Programming
date: 2009-08-28 19:16:19
---

昨天在写报名系统后台时，首先遇到的第一个问题是关于怎么将数据库中的内容在smarty中表现，因为平常在用PHP输出数据库内容时都是用类似while($row=mysql_fetch_array($sql_query)){.........}的方式进行输出，根据while中条件的执行次数而将内容依次往下读取，而用smarty进行这类数据输出时，需要提前将数组定义好。

第二个问题是关于分页，关于分页，我采取的是最简单的分页方式，当然可以视情况进行添加，也可以将我之前在博客中发表的一篇PHP分页函数加以修改用于smarty中。

首先来说第一个问题。

在smarty中，输出数组的循环数据的方式有几种，但我比较偏向于使用{section name=list loop=$title}   ｛/section}的方式进行输出，用smarty输出数组时，需要将数组进行定义，类似下面形式：

$menu[]=array("link"=&gt;"index.php","name"=&gt;"管理首页");
$menu[]=array("link"=&gt;"config.php","name"=&gt;"系统配置");
$menu[]=array("link"=&gt;"list.php?page=1","name"=&gt;"名单查看");

然后在模板中这样进行输出：

&lt;ul&gt;
{section name=list loop=$menu}

&lt;li&gt;&lt;a href="{$menu[list].link}" target="_self"&gt;{$menu[list].name}&lt;/a&gt;&lt;/li&gt;
{/section}
&lt;/ul&gt;

上面那段是我目前在做的报名系统中的后台菜单栏部分。

而通过PHP在数据库中读写出来的内容只是某一条的数据，所以需要用以往的方式将数据进行重新赋值，类似这样：

while($row=mysql_fetch_array($db_list_list)){

$page_list[]=array("id"=&gt;$row['link_id'],"url"=&gt;$row['link_url'],"name"=&gt;$row['link_name']);

}

其中，$page_list[]就是我们将数据库中的数据遍历过后并进行重新定义的数组，就类似之前的$menu[]变量，这个时候便可以用smarty输出数组的方式进行输出。

关于分页的问题，先简单的说说原理，其实在smarty中我们可以用{section}{/section}的参数进行分页处理，但那样个人觉得比较麻烦，而且模板文件也会编写的比较复杂。

关于分页我们可以将通获取url参数进行判断，并限制SQL查询数据，通过限制SQL的查询数据而控制smarty解析的内容。详细的思路我将写道下面的源码的注释中。

首先说明一下关于我的源码问题，源码中包含两个文件，PHP文件和html的smarty模板文件。其中不含有数据库，smarty的配置代码，‘wp_links‘是我在测试数据中使用的wordpress数据库中的友情连接部分。

<pre lang="PHP" line="1" file="download.txt" colla="+">
//首先是PHP文件部分。
<?php

require("include.php");   //包含smarty配置部分
require 'conn.php';        //包含数据库配置部分

$pagesize=10;        //设置每页数据显示数量

$url=$_SERVER['REQUEST_URI'];
$url=parse_url($url);
$url=$url['path'];

$sql="SELECT * FROM `wp_links`";
$db_list=mysql_query($sql);

$num=mysql_num_rows($db_list);    //统计数据总数
$pages=$num/$pagesize;
$pages=ceil($pages);           //求出一共需要多少页进行显示

if ($_GET['page']){
	$pageval=$_GET['page'];
	$page=($pageval-1)*$pagesize;
	}
if($num>$pagesize){
	if (!isset($pageval)) $pageval=1;
}

if ($pages==1){                  //如果总页面只有一页的话，将“上一页”“下一页”的标签替换为空。
	$pageup="";
	$pagedown="";

}else{
switch($pageval){
	case 1 :{
		$pageup="首页";
		$pagedown="[下一页]($url?page=)";
		break;
	}
	default :{
		$pageup="[上一页]($url?page=)";
		$pagedown="[下一页]($url?page=)";
	    break;
	}
	case $pages :{
		$pageup="[上一页]($url?page=)";
		$pagedown="末页";
		break;
    }

}

}$smarty->assign("pageconfig",$pageconfig);
//==================================================
$sql_list="SELECT * FROM `wp_links` LIMIT $page,$pagesize";        //由此控制数据显示数量部分
$db_list_list=mysql_query($sql_list);

while($row=mysql_fetch_array($db_list_list)){

	$page_list[]=array("id"=>$row['link_id'],"url"=>$row['link_url'],"name"=>$row['link_name']);      //将数据库中查询内容重新赋值

}

$pageconfig="当前第 $pageval 页,共 $pages 页";

$smarty->assign("pageconfig",$pageconfig);
$smarty->assign("pageup",$pageup);
$smarty->assign("pagedown",$pagedown);
$smarty->assign("title",$page_list);
$smarty->display("index.htm");

?>
</pre>

下面为模板的编写部分:
<pre lang="HTML" line="1" file="download.txt" colla="+">
<table>
 <tr>
 <td>id</td>
 <td>url</td>
 <td>name</td>
 </tr>
{section name=list loop=$title}
 <tr>
 <td>{$title[list].id}</td>
 <td>{$title[list].url}</td>
 <td>{$title[list].name}</td>

 </tr>
{/section}
 </table>

 {$pageup}{$pagedown}{$pageconfig}
</pre>