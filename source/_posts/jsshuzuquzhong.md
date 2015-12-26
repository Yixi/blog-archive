title: js数组去重
tags:
  - javascript
  - 数组
  - 算法
id: 1104
categories:
  - javascript
date: 2013-02-03 15:30:05
---

在看seajs源码的时候，看到里面一个数组去重的方法太巧妙了。

&nbsp;
<pre lang="Javascript" line="1" file="download.txt" colla="+">
//定义foreach。 ES5中数组扩展了foreach方法。

var forEach = util.forEach = AP.forEach ?
      function(arr, fn) {
        arr.forEach(fn)
      } :
      function(arr, fn) {
        for (var i = 0; i < arr.length; i++) {
          fn(arr[i], i, arr)
        }
      }

//去重算法
util.unique = function(arr) {
    //声明空数组ret，空对象o
    var ret = []
    var o = {}

    //将数组对象执行forEach方法，得到去重后的对象o
    forEach(arr, function(item) {
      o[item] = 1
    })

    //对象以键值数组化
    if (Object.keys) {
      ret = Object.keys(o)
    }
    else {
      for (var p in o) {
        if (o.hasOwnProperty(p)) {
          ret.push(p)
        }
      }
    }

    //返回数组
    return ret
  }

</pre>