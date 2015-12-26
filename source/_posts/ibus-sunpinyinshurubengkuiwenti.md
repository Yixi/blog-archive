title: ibus-sunpinyin输入崩溃问题。
tags:
  - Ibus
  - Linux
id: 574
categories:
  - 窗外的世界
date: 2010-03-17 10:54:46
---

我依然还是很勇敢很果断的把我的系统
> yaourt -Syu
了。

然后就囧了，因为ibus移到了源中，而且源中的ibus要比aur里面的ibus版本新。重新登陆linux后，发现只要一调出ibus-sunpinyin输入时，当前输入的窗口就会崩溃，关闭掉ibus后，输入窗口一同关闭。

后来排查后，是因为未更新aur中的ibus-sunpinyin的缘故，更新ibus-sunpinyin后问题解决。
> <span style="color: #ff0000;">yaourt ibus-sunpinyin</span>