title: ArchLinux双显示器拼接
tags:
  - Linux
  - 技巧
id: 399
categories:
  - 窗外的世界
date: 2009-10-20 10:22:41
---

老规矩，先上图。。

[caption id="attachment_401" align="alignnone" width="600" caption="工作台"]![工作台](http://blog.liuyixi.com/wp-content/uploads/2009/10/2009.jpg "工作台")[/caption]

昨天团队的人把显示器放到了这里，出于玩的心情，便想试试关于Linux下面的双显示器输出是怎样弄的，开始在插到外部显示器输出的接口上时，发现在系统的显示设置里面并没出现第二个显示器的一些设置项，最早在网上查找的时候便看到说ubuntu下面能够很方便的系统选项显示设置里面进行双显示器的配置，但archlinux下面的显示设置便没看到关于那些的设置。

<!--more-->

在网上查找办法，大部分的都说的是通过修改xorg.conf的配置文件来实现对显示器的管理工作，但修改这个配置文件着实麻烦，心想有没有软件能够实现简单的管理工作，到ArchLinux的wiki上面进行查找，但苦于不会做英语的关键词，所以不了了之。

在能够控制显示器的画面中瞎折腾时，偶然想到我还有个NVDIDIA X Server Settings这个工具，果然在里面的X Server Display Configuration中找到了新添加显示器的地方，添加后，系统自动识别出的我的外接显示器为BenQ FP71G 这个时候将Configure改成TwinView便可以实现显示器的拼接。

因为显示的分辨率现在变成了2560＊960，因为右边的笔记本只能显示高度800px，所以下面的还有160px的部分是看不到的，这是一个不够完美的地方。

[caption id="attachment_402" align="alignnone" width="324" caption="显示设置"]![显示设置](http://blog.liuyixi.com/wp-content/uploads/2009/10/1212.jpg "display")[/caption]

最近准备着手一个小型的cms系统的制作，主要是为了蛋哥的电视系统的在线页面的制作，涉及的方面比较简单，做一个小型的cms系统足够也，现在便准备开始数据库的构画。