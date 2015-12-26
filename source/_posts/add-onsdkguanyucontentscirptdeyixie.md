title: Add-on SDK 关于content scirpt的一些
tags:
  - add-on sdk
  - firefox
  - jetpack
  - 插件
  - 插件开发
id: 962
categories:
  - Firefox
date: 2011-09-09 11:27:34
---

Firefox 的Add-on SDK (jetpack)从1.0rc2版本开始后，对content script的机制有个重要的改动，现在不能在content script中直接来操作页面的dom 和监听DOM事件

但诡异的是，这个改动它并没有写到它的开发文档里面。虽然可能的原因是使用到这个用处的人并不多或者jetpack本就不提倡这样使用。

因为在Read Later Fast / Quick Note / Awesome Screenshot  for firefox 都使用到了这些东西，从而导致使用新的SDK build后的一些功能失效。

最初以为是BUG，去mozilla的bug系统搜时发现果然有这么一个说法：

[https://bugzilla.mozilla.org/show_bug.cgi?id=660780](https://bugzilla.mozilla.org/show_bug.cgi?id=660780)

后来看到release note中确实提到了关于content script的改动：
> We've changed the way content scripts interact with web pages, in order to improve security.> 
> 
> Previously, content scripts that accessed DOM objects in the page would frequently access the same objects as those being accessed by the page. This gives rise to two problems:> 
> 
> 1.  many changes to the page would be visible to the page, making it obvious to the page that an add-on was modifying it.
> 2.  a malicious page might redefine functions and properties of them so they don't do what the add-on expects. For example, if a content script calls`document.getElementById()` to retrieve a DOM element, then a malicious page could redefine its behavior to return something unexpected.> 
> To deal with these problems, DOM objects like the global window object are now implemented in a way that ensures that content scripts that access those objects will get the native implementations of their properties and methods.> 
> 
> Content scripts that modify those DOM objects will modify a proxy object instead of the real object.> 
> 
> &nbsp;
大致是说，为了安全性考虑云云，在content script与DOM交互的时候用到一个中间的代理。

但这个代理是什么却没有明确的说道，你需要去参考那个bug页面阅读后才明白是怎么回事。

简单点说，就是content script使用的页面的window对象不再是当前的window对象，而使用了一个代理的的 unsafeWindow 对象

如果这个变动导致你在content script中使用的document 或者jquery函数失效的话，你可以在content script中加上这么一句：

<pre lang="javascript" line="1" file="download.txt" colla="+">
var document=unsafeWindow.document,$=unsafeWindow.$;
</pre>