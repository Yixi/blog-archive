title: win7(vista)下恢复Linux引导并设置默认启动Linux.
tags:
  - Linux
  - 技巧
id: 544
categories:
  - 窗外的世界
date: 2010-02-01 12:38:35
---

关于这个，在网上有很多的办法，有一个比较通用的办法便是手动编写boot.ini放在c盘文件夹，但网上往往给出了这个办法，但却不能设置默认启动linux。

在这里先废话一下重装了windows 7后恢复Linux引导的办法。

首先在网上下载grub4dos工具，把文件包中的 grldr 和 grldr.mbr 文件放到C盘（系统盘）根目录下，然后在根目录中新建文件 boot.ini 编写下面的内容：
> [boot loader]> 
> [operating systems]> 
> c:\grldr.mbr="Archlinux"
重起后你就可以看到了效果，这时候在启动菜单中多了一个Archlinux的菜单，并正确的引导进入你的Linux系统。
> 你也可以下载我已经编辑好的三个文件，直接解压放到C盘根目录即可。> 
> 
> [点此下载](http://blog.liuyixi.com/upload/boot.tar.gz)
一般来说，这样便就可以了，但这里有一个不完美的地方，不能设置默认启动Linux ，即使在boot.ini中书写上defaut的代码。虽然大多数人或许用不到默认启动Linux，但对于我们这样主系统在Linux下的人来说，就比较麻烦了，每次开机的时候都要守到机器到选择启动菜单。

因为现在windows使用BCD来管理启动项，即使添加了boot.ini文件，但是在win7中系统启动选项中却依然只有windows7一个选项。

考虑到这点，我们便从BCD入手。

我们需要一个工具，[easyBCD](http://www.onlinedown.net/soft/58174.htm)，软件安装好后，选择 Add/Remove Entries选项，在下面添加一个Linux的启动菜单。

[![](http://blog.liuyixi.com/wp-content/uploads/2010/02/Capture.jpg "EasyBCD")](http://blog.liuyixi.com/wp-content/uploads/2010/02/Capture.jpg)

设置如图，这个时候你可以重起启动系统试试，如果在新出现的Arch Linux菜单中，能正确的引导进入你的Linux系统的话，那么就可以不用再做其他的了，并且可以删除之前在C盘的的boot.ini grldr grldr.mbr文件。并在windows 默认启动选项中选择新添加的Arch Linux即可。

但如果你的情况和我一样，新添加的Arch Linux并不能正确的引导进入Linux系统的话，那便将c盘的grldr.mbr文件拷贝至C:/NST/文件目录下，并将之重命名替换之前目录下的NeoGrub.mbr文件。然后重起，若是能成功的进入Linux , 那么可以删除掉c盘根目录下的boot.ini文件。然后在windows启动设置中选择Arch Linux默认启动即可。

当然，有人或许会质疑，为什么不用Live CD来恢复Grub 让Linux下的Grub来接管启动设置，当然这是一个比较好的办法，但是考虑到这样的情况，windows每次重装时，都会强制性的写入mbr，只要我们将boot.ini grldr grldr.mbr三个文件备份，每次重装后拷贝到c盘即可，而且我长期处于手里没有任何CD 或者U盘工具的情况下，我可以通过硬盘来完成重装系统，恢复引导。况且，linux重装的可能性比较小，而windows的重装可能性，大家就都知道了。