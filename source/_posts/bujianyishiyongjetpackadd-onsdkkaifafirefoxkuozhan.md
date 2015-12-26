title: 不建议使用jetpack(Add-On SDK)开发 Firefox扩展
tags:
  - Add-on
  - firefox4
  - jetpack
id: 820
categories:
  - Firefox
  - javascript
  - 工作记录
date: 2011-04-08 11:51:31
---

Firefox4现在正式版已经发布，虽然mozilla在推荐使用jetpack（Add-On SDK）来开发Firefox的Add-on，或许以后还会主要推荐使用jetpack来开发插件，从而慢慢抛弃以前传统的XUL的方式。但至少现在，我不推荐使用jetpack来开发插件，原因有下面几点。

1，UI的限制性

开发一个扩展，想好需求后，就要考虑你将扩展的入口放在什么位置，而Firefox的开放性，使用传统的开发方式可以几乎在Firefox的任何位置进行自定义。但如果使用jetpack开发，API提供的UI只有两个，一个是widget（即Firefox4的Add-on Bar），一个是context menu。Firefox4的add-on bar上面放一个icon非常的不显眼，且很容易被关闭，一旦关闭后，用户就很难再找到扩展的入口了。然后是context menu，jetpack中提供的参数很基本，比如你不能给context menu的前面加上icon。好吧这些都没事，但还有个更大的问题，扩展图标的位置不能自定义！虽然能拖到其他的各个位置，但拖动后你就会发现有各种的诡异问题。而且下一次重启后就会恢复原来的位置。

[![](http://blog.liuyixi.com/wp-content/uploads/2011/04/ff1.jpg "ff1")](http://blog.liuyixi.com/wp-content/uploads/2011/04/ff1.jpg)

看到没，因为使用jetpack生成的icon没有button的样式，拖上去后会导致toolbar压缩，很诡异。

关于图标入口位置的定义，当然接触过传统开发办法的童鞋可能会想到一个办法，使用XPCOM来插入。比如上图中右上角我的项目 Read Later Fast也是用jetpack开发的。

具体实现方式如下，首先引用jetpack中的chrome模块来调用XPCOM，然后通过XPCOM来向browser.xul插入DOM。
<pre lang="javascript" line="1" file="download.txt" colla="+">
var {Cc, Ci,Cu,Cr,Cm} = require("chrome");
var mediator = Cc['@mozilla.org/appshell/window-mediator;1']
.getService(Ci.nsIWindowMediator);
var win = win||mediator.getMostRecentWindow("navigator:browser");
  var doc =win.document;

  //add toolbar button
  var addonBar = doc.getElementById("nav-bar");
  if(addonBar!=undefined){
    var newItem = doc.createElement("toolbarbutton");
    newItem.setAttribute('tooltiptext','Read Later Fast');
    addonBar.appendChild(newItem);
    newItem.id = 'read-later-fast';
    newItem.className = "toolbarbutton-1 chromeclass-toolbar-additional";
    newItem.image= data.url('icon20.png');
    newItem.onmousedown = function(e) {
      if(e.which==1) tabs.open({url:data.url('RLF.html')});
    }
  }</pre>
这个方式比较诡异，虽然实现了在toolbar中插入icon，但是你在卸载或者禁用扩展时，icon并不会消失，在你新打开窗口时，新窗口中也没有icon的添加，对于这些情况你还需要写一些代码来特殊处理，如果需要了解，可以在评论中和我讨论。当然用这个方法，可以在firefox任何地方按照像以前XUL方式原理来自定义，但你需要花更麻烦的方法来处理带来的副作用，比如刚才提到的icon消失之类的问题。

2.扩展大小问题
<!--more-->
Read Later Fast chrome版本和firefox版本是用的同一份代码，只是各自的API和一些东西的实现方式不同，但chrome打包下来的大小只有300K大小，而firefox下的build下来520k，两者的本质都是zip文件。为什么差别会这么大？

这是因为使用jetpack开发扩展，在生成的时候会把所有的jetpack的js库包含进去，这些库文件解压后大小就占了530k左右

[![](http://blog.liuyixi.com/wp-content/uploads/2011/04/ff2.jpg "ff2")](http://blog.liuyixi.com/wp-content/uploads/2011/04/ff2.jpg)

这是一个用jetpack开发的buzz插件的resource文件夹下，其中由开发者写的入的代码在第5个文件夹下，大小1.4k，而上面的四个文件夹都是由于build插件时build进去的，四个文件夹大小共520K，最后build出来的cfx插件文件大小189k，而实际书写了代码的部分只有1.4k。

3.jetpack本身的bug以及和一些插件的冲突。

先说插件冲突吧，有一个firefox 的扩展 tab mix plus ，当使用这个扩展提供的恢复会话时，重启firefox，所有使用jetpack开发的扩展都不能正常启动，必须手动在扩展管理页面把手动禁用然后启用才能正常运行。这个问题不是代码的问题，确确实实是一个问题。不管是jetpack的问题还是tab mix plus的问题，但有一个问题需要注意，tab mix plus的用户估计比所有使用jetpack开发的扩展的用户总量还要多，因为jetpack开发的扩展实在不多。

这个BUG我已分别提交到tab mix plus和jetpack：

[http://tmp.garyr.net/forum/viewtopic.php?p=48307](http://tmp.garyr.net/forum/viewtopic.php?p=48307)

[https://bugzilla.mozilla.org/show_bug.cgi?id=646767](https://bugzilla.mozilla.org/show_bug.cgi?id=646767)

jetpack本身也存在一些BUG，一个是和firefox4的tab group冲突，然后是popup窗口关闭时的bug。这两个问题在使用最新的SDK中已经修复，用最新的SDK build一下问题就消失。或许像这样的问题还有更多我们没发现。

--------分割线-----------------------------

当然说了这么多的不好，jetpack还是有很多优点的，比如可以很快速的开发扩展，比起之前的XUL方式，使用jetpack开发确实快的多。然后就是调试也很方便，还有其他的就不多说了。总之我还是不建议目前使用jetpack来开发firefox的扩展。

---------------------------

今天中午的时候，看到tab mix plus发布的新版本，已经修复了上面提到和jetpack冲突的问题
http://tmp.garyr.net/forum/viewtopic.php?t=10888