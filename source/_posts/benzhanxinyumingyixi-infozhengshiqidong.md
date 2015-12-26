title: 本站新域名 yixi.info 正式启动
tags:
  - 博客
id: 520
categories:
  - 网络琐事
date: 2010-01-23 18:07:58
---

我终于不执迷不悟了，CN 不靠谱啊不靠谱。不靠谱啊不靠谱。

国内主机也不靠谱啊不靠谱。

昨天小汐帮忙注册了 yixi.info 的域名，今天正式启动了，请看到这篇文章且和小站做了友情链接的更换一下友情连接，劳烦了 ^_^

感谢google,感谢wordpress中文论坛的众牛，让我找到了更换域名的办法

1，将新域名解析到主机。

2，请果断备份更改域名前的MySQL数据.

3，进入WordPress后台设置更改“Wordpress安装地址”和“博客地址”。

4，在phpMyAdmin中更换数据库中以前的网址链接内容

<pre lang="SQL" line="1" file="download.txt" colla="+">
--替换文章中的内部链接。
UPDATE wp_posts SET post_content=REPLACE(post_content,'http://www.liuyixi.cn','http://blog.liuyixi.com');
UPDATE wp_posts SET post_content=REPLACE(post_content,'http://liuyixi.cn','http://blog.liuyixi.com');
--替换文章的永久链接
UPDATE wp_posts SET guid=REPLACE(guid,'http://www.liuyixi.cn','http://blog.liuyixi.com');
UPDATE wp_posts SET guid=REPLACE(guid,'http://liuyixi.cn','http://blog.liuyixi.com');
--替换评论中的链接
UPDATE wp_comments SET comment_author_url=REPLACE(comment_author_url,'http://www.liuyixi.cn','http://blog.liuyixi.com');
UPDATE wp_comments SET comment_author_url=REPLACE(comment_author_url,'http://liuyixi.cn','http://blog.liuyixi.com');
</pre>

5，301重定向,将使用原域名对本站的访问都转移到新域名，尤其对搜索引擎优化有益。(因为本人不太擅长，此部分为网上搜索，且本站目前截止还未做301重定向）

> 在主机支持.htaccess的前提下，修改Web根目录下的.htaccess文件，加入如下内容：> 
> 
> RewriteEngine On> 
> RewriteCond %{HTTP_HOST} ^liuyixi.cn [NC,OR]> 
> RewriteCond %{HTTP_HOST} ^www.liuyixi.cn [NC]> 
> RewriteRule ^(.*)$ http://blog.liuyixi.com/$1 [L,R=301]

谷歌那边，我已经提交了网址更换申请，至于百度，那就无视了。