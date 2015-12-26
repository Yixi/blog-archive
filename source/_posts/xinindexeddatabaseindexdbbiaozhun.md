title: 新Indexed Database(indexdb)标准
tags:
  - HTML5
  - indexdb
id: 1042
categories:
  - HTML5
date: 2012-03-08 10:59:46
---

W3c在去年12月6日时对indexdb的草案做了一些修改，虽然变动不是很大，但是却直接使得以前的代码不能正常work，主要在数据库创建的部分。

目前firefox10以后以及ie10(windows8 Consumer Preview)支持此标准，chrome未测，未知，但未来应该都会遵循这个标准。

具体的可以参考w3c的官方文档，地址在这里 ：[http://www.w3.org/TR/IndexedDB/](http://www.w3.org/TR/IndexedDB/)

**在网上查找关于indexdb的教程的也需注意查看时间，如果是针对firefox10之前的代码或者12月6日前的代码在最新的浏览器上是不能正常work的。**

写这篇文章本来是要填之前在那边win8的文章里说IE10里面indexdb bug那个坑的。后来重构的时候，发现这并不是BUG，是遵循的标准程度不一样的原因。而伴随着前几天windows8 consumer preview新出来的IE10已经遵循最新的indexdb标准，所以代码已经和firefox一样，所以这里不再理会那个所谓的bug.这里重点讲下新的数据库声明方式（这是变动部分），而是用indexdb的方法并没有变动。

比较大的一个变动部分是废弃了以前的 setVersion()方法，所以导致我们在创建数据库和createObjectStore的流程有一些变动，而且多了一些新的回调方法。

首先是创建数据库

<pre lang="Javascript" line="1" colla="+">
var DB={};
window.indexedDB = window.indexedDB || window.webkitIndexedDB || window.mozIndexedDB; //各浏览器的各自的私有方法，这个不多说了；
DB.openDatabase(function(){
   console.log('Database open');   //数据库初始化完成后我们回到这里。
});
DB.openDatabase = function(callback) {
   var request = indexedDB.open('quicknote',1);   //注意区别以前的方法，这里第二个参数不再是description，而是数据库版本号
   request.onsuccess = function(e) {     //数据库打开成功回调
       DB.db = e.target.result;    //我们用DB.db来存放indexdb
       callback();
   };

   request.onupgradeneeded = function(e){    //第一次打开数据库或数据库升级时会触发，完成后根据情况触发success或者error
       DB.db = e.target.result;
       var db = DB.db;
       if(!DB.db.objectStoreNames.contains('notes')){    //createObjectStore,以前需要在setVersion时才能执行。
	/* create object store*/
	  db.createObjectStore('notes', {keyPath:'id', autoIncrement:true})
	      .createIndex('updated', 'updated', { unique: false });
       }
   };

   request.onerror = function(e){   //数据库打开错误回调
       console.log(e);
   }
}
</pre>

上面就是新的indexdb的数据库初始化方式，相对以前的来说，代码简化了不少，也不用人为的判断数据库版本号了。