title: javascript DOMNodeInserted事件
tags:
  - DOMNodeInserted
  - 技巧
id: 936
categories:
  - Chrome
  - Firefox
  - javascript
date: 2011-07-27 15:21:33
---

最近一个插件的功能需求，需要在第三方的ajax载入回来的内容中通过contentscript来插入一些我们的内容。

在什么时候去插，这是个很麻烦的问题。

因为要使插入这个动作生效，那在执行插入时，被插入的DOM部分一定是已经load完成的。之前试过第一次插入时，通过setTimeout来循环判断DOM是否已经在页面上，然后在进行插入。这个办法解决的第一次时候能够正常插入，但是在页面不刷新的情况下，又一次ajax载入的内容就不会生效了。

想到了去捕捉ajax完成后的触发某一事件，但好像并没有哪一种方法能够实现，倒是让我发现了 DOMNodeInserted 事件。

DOMNodeInserted 从字面理解比较简单，就是每次页面有DOM插入时都会触发。

运用这个事件，提到的需求就变的简单了，我只要在每次触发这个事件获取到的event.target，判断其DOM内容是否有我将要插入部分的结构特征然后来进行插入就行了。

与这个事件成对的还有一个 DOMNodeRemoved 事件。

有兴趣的话，可以在W3C中查找相关资料。当然这个时间IE是不支持的，在IE下要实现开头提到的需求，估计还是得要用setTimeout来循环监听。