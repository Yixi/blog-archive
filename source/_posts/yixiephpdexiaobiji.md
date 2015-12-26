title: 一些PHP的小笔记
tags:
  - PHP
  - 笔记
id: 637
categories:
  - PHP Programming
date: 2010-07-26 10:04:12
---

<span style="color: #800000;">**require() 与 include()的区别**</span><span style="color: #800000;">：</span>

<span style="color: #800000;"> </span>require() 函数与 include() 相同，不同的是它对错误的处理方式。include() 函数会生成一个警告（但是脚本会继续执行），而 require() 函数会生成一个致命错误（fatal error）（在错误发生后脚本会停止执行）。

<span style="color: #800000;">**关于一些文件操作函数：**</span>

feof() 函数检测是否已达到文件的末端 (EOF)，fgets() 函数用于从文件中逐行读取文件，fgetc() 函数用于从文件逐字符地读取文件。