title: Audio Player不显示问题
tags:
  - Audio Player
  - Wordpress
  - 博客
  - 插件
id: 852
categories:
  - 网络琐事
date: 2011-04-28 16:42:52
---

发现博客还有这个插件

[audio:http://product.3g.21cn.com/ct_hub/music/008.mp3|autostart=yes|loop=yes]

这玩意半年未一直都不显示，google了一下，找到了解决办法：

检查模板header.php的&lt;/head&gt;前是否有&lt;?php wp_head(); ?&gt;
检查模板footer.php的&lt;/body&gt;前是否有&lt;?php wp_footer(); ?&gt;

使用参数

Option	Effect
autostart=yes	是否自动播放(默认设置为 no不自动播放)
loop=yes	是否循环播放 (默认设置为 no 不循环播放)
bg=0xHHHHHH	背景色设置(在 HHHHHH 的地方用颜色代码替换如 FFFFFF或009933等)
leftbg=0xHHHHHH	左背景色
rightbg=0xHHHHHH	右背景色
rightbghover=0xHHHHHH	鼠标经过时右背景色
lefticon=0xHHHHHH	左图标色
righticon=0xHHHHHH	右图标色
righticonhover=0xHHHHHH	鼠标经过时右图标色
text=0xHHHHHH	文字色
slider=0xHHHHHH	播放轨迹指示滑块色
loader=0xHHHHHH	播放轨迹已播放部分背景色
track=0xHHHHHH	播放轨迹为播放部分背景色
border=0xHHHHHH	播放轨迹边框色

&nbsp;