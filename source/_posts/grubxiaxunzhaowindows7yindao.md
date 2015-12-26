title: grub下寻找windows7引导
tags:
  - Linux
id: 588
categories:
  - 窗外的世界
date: 2010-04-12 23:22:47
---

今天引导又莫名其妙的出问题，直接就进入了linux的grub，即使选择windows选项也直接跳转回来。
不知道是动到了哪个地方，尝试手动引导，还好成功了。
具体方法，在grub菜单下按C进入Grub命令行。
输入：

> grub>find --set-root /bootmgr> 
> grub>chainloader /bootmgr> 
> grub>boot