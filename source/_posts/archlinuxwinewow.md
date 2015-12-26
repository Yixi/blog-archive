title: 'Arch Linux wine WOW '
tags:
  - Linux
  - 技巧
id: 316
categories:
  - 工作记录
  - 窗外的世界
date: 2009-08-19 20:22:12
---

百无聊赖时，想玩游戏，因为之前分区的时候，为了更方便的转移数据，所以将电脑中的游戏基本上都进行了删除，只留下了一个魔兽世界，因为确实太大，删除了于心不忍，前面知道Linux下能够用wine进行运行，据说还比较流畅，但真正到了Linux下才发现相当的纠结，安装好后，运行wine wow.exe时，窗口弹开后然后就关闭了。

好了，废话不多说，现在说说怎么用wine运行魔兽世界吧。

如果是全新安装魔兽世界的话，推荐到电驴上下载一个 Cedega 进行管理，详细就不多说了。

因为我是从windows转到Linux下，WOW是之前就在windows下安装好的，按照下面的步凑进行。

Arch linux下：

1\. 安装 wine

终端下：  pacman -S wine

等待自动安装。

2\. 安装好后，在终端下输入： regedit 打开wine的注册表。

找到HKEY_CURRENT_USER\Software\Wine\OpenGL

没有OpenGL进行手动添加目录。

新建一键值：“DisabledExtensions”

值为：”GL_ARB_vertex_buffer_object”
3.找到魔兽世界目录下的WTF目录下的Config.wtf，在最后面添加下面的代码：

SET gxApi "opengl"
SET gxCursor "0"
SET textureFilteringMode "0"
SET baseMip "1"
SET groundEffectDist "70"
SET SoundOutputSystem "1"
SET SoundBufferSize "150"

最后在终端下运行魔兽世界：

wine /.../wow.exe -opengl

到这里，就能运行魔兽世界了。

需要注意的是，wine下对硬件的驱动没有windows下好，所以尽量关闭游戏的特效以保证游戏的流畅运行，而且需要关闭Linux桌面本身的特效。