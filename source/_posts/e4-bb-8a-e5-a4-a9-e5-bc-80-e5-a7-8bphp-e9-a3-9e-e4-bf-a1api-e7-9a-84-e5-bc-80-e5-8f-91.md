title: 今天开始PHP飞信API的开发
tags:
  - API
  - PHP
id: 182
categories:
  - 工作记录
date: 2009-06-07 19:19:20
---

因为项目计划中有需要用到短信及时发送的功能要求，想到前段时间在WordPress中文论坛上看到一个插件，利用飞信的API来实现博客有评论的时候给博主发送短消息的功能，所以想到利用飞信的API也能实现我要的功能了。

网上虽然已经有做好的飞信API接口，但因为为明文存放，并不安全，而且我所需要的功能也并不是简单的发送短消息而已。

在网上搜索的时候，说是CSDN上有PHP的飞信类，开始很郁闷，下了一个是Symbian的飞信接口文档，很厚的一本文档。后来总算是找到了PHP飞信类，一共是三个PHP文件。

在测试的时候，运行报错，因为要使用PHP飞信类需要两个PHP中的curl的扩展和socket扩展，默认中这两个扩展是未被PHP支持的，从而无法正常的运行飞信PHP类中的方法。

开启curl和socket扩展的方法：

首先确定Windows下面看看ext目录下面有没有php_sockets.dll和php_curl.dll文件。

然后在php.ini中找到

;extension=php_curl.dll

;extension=php_sockets.dll

将这两个语句前的分号去掉，或者直接添加两行：

extension=php_sockets.dll

extension=php_curl.dll

然后重启apache

linux好像是ext/php_sockets.so的扩展，或者按照那个报错的说的在config时使用--with-socket重新编译下php

在网站系统中镶入实时的短信提醒功能后，就能够实现很多的现实生活中需要的功能。

关于我重写的无提示消息的飞信PHP类下载：

-------------------------------------------------------

[PHP飞信类重写版下载](http://blog.liuyixi.com/index.php/2009-07/267)

-------------------------------------------------------