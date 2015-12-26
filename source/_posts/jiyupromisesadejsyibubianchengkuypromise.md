title: 基于Promises/A的js异步编程库 YPromise
tags:
  - commonJS
  - nodejs
  - promise
  - 异步
id: 1120
categories:
  - javascript
date: 2013-10-12 12:09:18
---

所有前端开发者被js的异步编程折腾不是一天两天的事，复杂的回调嵌套和回调条件判断都会产生一些不易于阅读维护甚至潜藏问题的代码。

Common JS提出了一种 Promises/A的建议来解决这个问题，一是易于阅读维护，其次是防止回调堆栈太深错误不易抛出的问题。

现在成熟的库都有自己的基于Promise的实现，比如jQuery的deferred机制，但感觉用起来最顺手和直观的还是在做win8开发时的WinJS实现的promise机制，后来终于有空尝试基于winJS的设计实现了一个简单的Promise库。

[https://github.com/Yixi/YPromise](https://github.com/Yixi/YPromise)

简单使用如下，更详细的请参考github
<pre lang="javascript" line="1" file="download.txt" colla="+">
function fun3(){
     return new YPro(function(comp,err){
        setTimeout(function(){
             comp('fun3 done');
        },3000);
     })
}
function fun4(){
     return new YPro(function(comp,err){
        setTimeout(function(){
             comp('fun4 done');
        },1000);
     })
}
var aPromise = fun3()
                .then(function(d){console.log(d); return fun4();})
                .then(function(){return fun3();})
                .then(function(){return fun4();})
                .done(function(){
                    console.log("fun3->fun4->fun3->fun4 done");
                })

setTimeout(function(){
    aPromise.cancel(function(){
        console.log("Promise canceled");
    });
},9000);

</pre>