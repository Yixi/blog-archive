title: Javascript复制JSON数据
tags:
  - JSON
id: 1048
categories:
  - javascript
date: 2012-04-11 14:23:50
---

复制数据很简单。

var a = jsonobj;

简单的就将jsonobj的值复制到了变量a中，但如果jsonobj是个json数据的话，你会发现修改a的值时，jsonobj也会跟着改变。

如果你对javascript中的prototype那套机制比较了解的话可能就会大概明白是怎么回事，是的，因为json其实也是个object，所以var a = jsonobj 赋值时，中间有个原型链会将两个关联起来。

要达到想要的复制数据也很简单：
> var a = JSON.parse(JSON.stringify(jsonobj));
将json序列化为string再还原成json，因为中间产生了新的对象，所以两者不再关联。

这种写法看起来很不科学，但应该是比较好的办法了。