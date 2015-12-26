title: jetpack add-on customize实现办法
tags:
  - firefox4
  - hack
  - jetpack
  - Read Later Fast
  - 技巧
id: 833
categories:
  - Browser
  - Firefox
  - 工作记录
date: 2011-04-12 15:06:58
---

前面有一篇关于不建议使用jetpack来开发firefox add-on的文章，无奈，手里的项目已经是jetpack的东西，所以只能一条路走到黑。
之前有提到说使用jetpack开发的add-On用户不能自定义add-on的位置，这两天查了下MDN，发现XUL有一个叫customization的事件（[https://developer.mozilla.org/en/XUL/Toolbars/Toolbar_customization_events](https://developer.mozilla.org/en/XUL/Toolbars/Toolbar_customization_events)），感觉应该有办法来实现使用jetpack开发的add-on的自定义。

_<span style="color: #993300;">注：使用下面说到的方法前提是你是使用我之前提到的插入button的方法，而不是使用jetpack的widget方法，参考：[http://blog.liuyixi.com/index.php/820](http://blog.liuyixi.com/index.php/820)</span>_

_<span style="color: #993300;">[](http://blog.liuyixi.com/index.php/820)</span>_
实现自定义首先需要把我们创建的DOM注册到自定义面板中：
<pre lang="javascript" line="1" file="download.txt" colla="+">
doc.getElementById("navigator-toolbox").palette.appendChild(newItem);
</pre>
注册到面板中后
因为我们的button是通过创建DOM的方式添加到toolbar上面的，所以只要记住自定义后add-on的位置，然后下一次添加DOM的时候根据这个记住的位置添加即可实现。

具体如下：

首先我们需要在simple-storage中初始化一些值，用于判断第一次安装时插入的位置，这部分的代码只需要执行一次，故在前面加上了一个if判断

<pre lang="javascript" line="1" file="download.txt" colla="+">
var s_flag = simpleStorage.storage.storagecreate;
if(s_flag!=1)
{
  console.log('initstorage');
  simpleStorage.storage = {
    b_parent:'nav-bar',
    b_next:null,
    storagecreate:1
  }
}
</pre>

然后是添加button部分的代码：
<pre lang="javascript" line="1" file="download.txt" colla="+">
 var win = win||mediator.getMostRecentWindow("navigator:browser");
  var doc =win.document;
  //add toolbar button
  var newItem = doc.createElement("toolbarbutton");
  newItem.setAttribute('tooltiptext','Read Later Fast');
  newItem.id = 'read-later-fast';
  newItem.className = "toolbarbutton-1 chromeclass-toolbar-additional";
  newItem.setAttribute('image',data.url('icon20.png'));
  newItem.onmousedown = function(e) {
    if(e.which==1) tabs.open({url:data.url('RLF.html')});
  }
  doc.getElementById("navigator-toolbox").palette.appendChild(newItem);
  var b_parent = simpleStorage.storage.b_parent;
  var b_next = simpleStorage.storage.b_next;
  console.log(b_parent,b_next);
  if(b_next!=null){
    var before = doc.getElementById(b_next); 
  }else{
    var before = null;
  }
  if(b_parent!=null){
    var parentNode = doc.getElementById(b_parent);
    parentNode.insertItem('read-later-fast', before, null, false);
  }
</pre>
最后是监听自定义add-on位置的代码，原理是当用户完成自定义事件时，触发aftercustomization事件，这个时候记录下我们插件的parentNode ID 和 nextSibling的ID，下次添加的时候便根据这两个位置来添加以实现保存位置的目的。需要注意的是，当用户把button拖回到面板中时，这个时候是无法获取到dom的，所以将记录的位置赋值为null：
<pre lang="javascript" line="1" file="download.txt" colla="+">
var win_cus = mediator.getMostRecentWindow("navigator:browser");
win_cus.addEventListener("aftercustomization", customizeEnd, false);
var doc_cus =win_cus.document;

function customizeEnd(e) {
  let theToolbox = e.target;
  var rlf = doc_cus.getElementById('read-later-fast');
  if(rlf==null){
    simpleStorage.storage.b_parent=simpleStorage.storage.b_next=null
  }else{
    simpleStorage.storage.b_parent = rlf['parentNode'].id;
    simpleStorage.storage.b_next = rlf['nextSibling'].id;
  }
  storagecreateflag = simpleStorage.storage.storagecreate;
}
</pre>