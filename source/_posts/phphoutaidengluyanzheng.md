title: PHP后台登陆验证
tags:
  - PHP
id: 292
categories:
  - PHP Programming
  - 工作记录
date: 2009-08-01 22:24:19
---

网站开发到现在，已经是开始细节上的完善，首先考虑到的第一个便是网站后台的安全性问题，在网上查找了一些文档，觉得，简单的后台验证可以这样实现。

首先准备一个公共验证页：

<pre lang="php" line="1" file="download.txt" colla="+">

if (!$_SESSION['adminname']){ 
echo " <script>alert('未登录，请返回登录页面！');location.href='login.html'; </script>"; 
exit;
}

</pre>

这是最简单的写法，然后将后台的每个页面将此文件include一次，便可以实现后台登陆的验证。考虑到安全性的问题，推荐使用session而不使用cookie。

当然，如果你觉得这样的安全性并达不到你的要求，你可以考虑添加类似IP，权限限制之类的代码。

在不同的情况下可以考虑到不同的情况做相应的安全设施。

由于我的这个站点只为实现以个功能，后台其实也并没有什么实质性的东西，所以用一个session来认证完全可以达到我的要求。