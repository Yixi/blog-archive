title: Linux下锐捷上网解决方案。
tags:
  - FORFUN
  - Linux
  - 网络
id: 321
categories:
  - 窗外的世界
date: 2009-08-25 05:35:32
---

凌晨四点50分现在。比较兴奋，终于解决了锐捷在Linux的认证问题，外面闪着猛雷，压抑不住内心的激动，记下这篇心得。

从去年开始就开始在关注Linux下瑞解的解决方案，官方有个Supplicant For Linux V1.1.1 但只能解决到ruijie3.32版本，我们入学的时候，学校好像刚换到ruijie3.35的动态DHCP认证，在windows下多了一个 802.1x的进程，纠结的事情就出在这个进程上面，Linux下很难解决这个问题。

大概是前面不久，小夕告诉我在google code上有个ruijieclient的开源程序，说是可以解决了ruijie3.35以上的认证问题，当时使用的是ubuntu,要在无网络下的情况解决那些依赖问题着实麻烦，后来便放弃了。

直到这几天，因为要回学校，不得不重新关注起这个问题。

ruijieclient 到现在已经发行到了0.8.1，昨天我在准备回学校的时候，从小汐的电脑上拷贝过来了ruijieclient0.7.9的archlinux安装包文件（因为google code 上的 ruijieclient都没有提供能直接在archlinux下安装的包文件）。

今天下午｀因该是昨天下午了，昨天下午回到学校的时候，开始着手准备认证的问题，中间出现了许多莫名其妙的问题，在xp和Arch Linux下重启换来换去无数次，无关紧要的我便不在述说。

理论上，ruijieclient到现在的发行版本都能够解决了锐捷登录的问题。

http://code.google.com/p/ruijieclient/

但我在使用时，系统提示“不允许使用的客户端类型”，虽然开发者说ruijieclient能够支持客户端版本欺骗，但却不成功，发现在google code上面有人遇到和我一样的问题。

因为可能学校的认证服务器打开了802.1x的MD5校验，所以ruijieclient没能够成功的欺骗，然后发现了这款软件MentoHUST.

http://pcyard.qupan.com/?folder=1117507

这款便能够成功的欺骗过锐捷的版本认证。

简单说下操作过程:

首先在windows下面下载文件

http://forum.ubuntu.org.cn/download/file.php?id=75607&amp;sid=ac5a2cc7663fbc7861fcaf1d986edd46

运行时可能会报错说缺少一个DLL组建，到网上搜索一下，下载后放到system32下面。

然后在上面的趣盘中下载对应学校使用锐捷版本的MPF文件和linux程序文件。

在软件中载入对应版本的MPF文件，然后点开始抓包，这个时候开始正常在windows下面登录锐捷，锐捷登录成功后，抓包完成，保存文件。

回到Linux下面首先需要准备一个包:可以手动到源里面下载：

libpcap-1.0.0-1-i686.pkg.tar.gz

在Linxu下，首先用pacman安装上面的软件包。

然后在/etc/下面新建一个文件夹 mentohust

将抓取的MPF包文件和linux程序文件包中的配置文件mentohust.conf拷贝到   /etc/mentohust/中

为了方便，将主程序MentoHUST拷贝到  /bin  中。

这个时候按照你在windows下的配置，按照说明配置好mentohust.conf中的内容。

其中Package的路径为指向抓取的那个MPF包文件。

配置好后，在终端中运行 MentoHUST

这个时候如果提示错误，没有找到   libpcap.so.0.9  的话，那么在终端中输入下面那句：

ln -s /usr/lib/libpcap.so.1  /usr/lib/libpcap.so.0.9

然后再执行，这个时候应该能够成功的登录锐捷了。锐捷3.35测试通过，以后版本请自测.

(待我整理好后，会给出上面提到的所有下载)

－－－－－－－－－－－我是华丽的分割线－－－－－－－－－－－－－－－
[root@localhost ~]# MentoHUST

欢迎使用MentoHUST    版本: 0.2.0
Copyright (C) 2009 HustMoon Studio
人到华中大，有甜亦有辣。明德厚学地，求是创新家。

** 用户名:    2008113577
** 网卡:    eth0
** 网关地址:    0.0.0.0
** DNS地址:    0.0.0.0
** 数据包:    /etc/mentohust/3_35.mpf
** 认证超时:    3秒
** 响应间隔:    30秒
** 自动重连:    240分钟
** 组播地址:    私有
** DHCP方式:    认证后
** DHCP脚本:    dhclient
** 本机MAC:    00:22:15:2e:75:72
** 使用IP:    10.20.14.32
** 子网掩码:    255.255.254.0
&gt;&gt; 寻找服务器...
** 认证MAC:    00:1a:a9:06:7b:12
&gt;&gt; 发送用户名...
&gt;&gt; 发送密码...
** 客户端版本:3.35 适用:Windows 类型:2
** MD5校验值:    95487c7df16c637320c4316b7f18c292
&gt;&gt; 认证成功!
$$ 计费信息:    您当前使用的服务为st_room,账户余额为0.00元;
计费策略为学生宿舍包月;
&gt;&gt; 正在获取IP...
Internet Systems Consortium DHCP Client V3.1.2p1
Copyright 2004-2009 Internet Systems Consortium.
All rights reserved.
For info, please visit http://www.isc.org/sw/dhcp/

can't create /var/state/dhcp/dhclient.leases: No such file or directory
Listening on LPF/wlan0/00:1f:3c:8d:ab:54
Sending on   LPF/wlan0/00:1f:3c:8d:ab:54
Listening on LPF/eth0/00:22:15:2e:75:72
Sending on   LPF/eth0/00:22:15:2e:75:72
Sending on   Socket/fallback
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 6
DHCPOFFER from 10.20.15.1
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPACK from 10.20.15.1
can't create /var/state/dhcp/dhclient.leases: No such file or directory
bound to 10.20.14.32 -- renewal in 14008 seconds.
&gt;&gt; 操作结束。
** 本机MAC:    00:22:15:2e:75:72
** 使用IP:    10.20.14.32
** 子网掩码:    255.255.254.0
&gt;&gt; 发送心跳包以保持在线...