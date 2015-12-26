title: 终于把系统更新了。
tags:
  - ArchLinux
  - Linux
id: 558
categories:
  - 窗外的世界
date: 2010-02-25 18:53:45
---

过年回家后，系统大概一个多月未更新。回到学校后果断的pacman -Syu

然后就出现了

kdelibs: requires phonon

网上google了一下，看到了官方给出了解答
> <pre>% pacman -Sy --asdeps qt> 
> % pacman -Su</pre>
可照做后，依然会出现同样的提示，在官方的论坛查了一下，有人说是先同步官方源的数据包，但照做后依然会有同样的提示。

便没有再管，挑出了部分不需要依赖qt的软件更新。

今天仔细查看了官方的论坛（悲剧我的英语水品），找到了解决的办法。
> <pre><span style="color: #ff0000;">$sudo pacman -S phonon --asdeps qt> 
> $sudo pacman -Syu</span></pre>
终于将系统更新了，内牛满面啊，看来是应该好好的看看pacman的手册了。