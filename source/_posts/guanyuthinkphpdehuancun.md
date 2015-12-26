title: 关于ThinkPHP的缓存
tags:
  - ThinkPHP
  - 开发
id: 673
categories:
  - PHP Programming
date: 2010-08-16 18:30:55
---

昨天在使用TP的AR模式更新数据时，就是在create()后使用 M('xxx')-&gt;field 来更新字段值时，老是更新不进去，开始以为是手册哪里没有讲这个方法讲明白，经过后面的排查才发现是因为缓存问题。

因为我在中途更新了表，添加了一个新的字段，而这个字段没写入缓存，删除runtime文件夹下内容后正常。

闲心的时候我看了下runtime目录下的东西。

有4个文件夹， Cache,Data,Logs,Temp，然后是~app.php  和 ~runtime.php 文件。

Cache下生成的PHP文件是模板的缓存，而Data文件夹下有个_fields的文件夹，里面存放的便是对应的Model的表的自动填充字段规则，比如：

<pre lang="PHP" line="1" file="download.txt" colla="+">
<?php
return array (
  0 => 'id',
  1 => 'title',
  2 => 'imageurl',
  3 => 'username',
  4 => 'cid',
  5 => 'postdate',
  6 => 'content',
  7 => 'good',
  '_autoinc' => true,
  '_pk' => 'id',
);
?>
</pre>

也是因为这两个文件就是导致开头我说的问题的原因了，修改了数据表后，缓存的Data并没有更新。

~app.php文件中保存是各种的系统配置，以及一些自定义的配置。