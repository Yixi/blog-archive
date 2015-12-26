title: Linux下硬盘安装win7
tags:
  - ArchLinux
  - Linux
  - win7
id: 871
categories:
  - 窗外的世界
date: 2011-05-04 17:03:04
---

劳动节没带电脑回家，从家里回到公司这边时，如往常一般开电脑，悲剧在这个时候发生了，在过了win7的启动画面后，电脑蓝屏，然后自动重启。

尝试启动双系统中的Arch Linux,启动时在挂在硬盘的时候提示非安全从windows关机，然后提示fixed.之后能进入linux系统，重启后依然不能进win7，故障依旧。

这个时候很纠结，因为手里没有U盘，光驱又是坏的，工作环境又在win7下。只有唯一的一个选择，从linux下硬盘重装win7。
从网上查了点资料，知道了大概的原理后，开始动手。

安装过程中需要 win7的镜像，grub4dos,easyBCD.

1，挂载win7镜像
<pre lang="bash" line="1" file="download.txt" colla="+">
$ sudo mkdir  /media/win7

$ sudo mount /media/soft/win7.iso /media/win7 -o loop
</pre>
先新建个挂载点，然后将iso文件挂载到新建的文件夹下，然后打开这个目录，将所有文件复制到一个nfts的根目录下,即对应win下 D盘，E盘，F盘的地方，因为C盘将要用来安装系统，所以我复制到了F盘中.

2，解压出grub4Dos的grub.exe

修改/boot/grub/menu.lst,添加如下几行：
<pre lang="grub" line="1" file="download.txt" colla="+">
title grub4dos
root (hd0,6)
kernel /home/grub.exe
boot
</pre>
其中第二行的root(hd0,6)根据自己linux所在硬盘的物理位置修改，具体可以参照menu.lst前面的内容。grub.exe修改为解压的路径。

3，重启后，在启动界面选择grub4dos，然后按c键进入grub&gt;模

依次输入以下指令:
<pre lang="grub" line="1" file="download.txt" colla="+">
grub>find --set-root /bootmgr

grub>chainloader /bootmgr

grub>boot
</pre>
随后进入win7安装界面，一路安装下去。

4，安装easyBCD恢复linux的引导。软件比较简单，尽量使用最新版的。

=====分割线====

如果你运气比较好的话，启动win7还能进入win7自带的诊断工具的话，完成了第一步解压后，在诊断工具中打开DOS工具，直接跳转到F盘，然后执行setup.exe便可以开始系统安装了。