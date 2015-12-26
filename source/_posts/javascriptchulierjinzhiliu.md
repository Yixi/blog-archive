title: javascript 处理二进制流
tags:
  - HTML5
  - 二进制
id: 1005
categories:
  - javascript
date: 2011-10-27 17:19:02
---

在javascript中，二进制流一般是一个[object ArrayBuffer]的对象，一般的javascript方法是没法处理这个object的。

要处理它，我们需要用Uint8Array将它转换成一个8位的整形数组。

当然，如果你需要，你还能将它还原成string

<pre lang="Javascript" line="1" file="download.txt" colla="+">
// t is a arraybuffer

var uInt8Array = new Uint8Array(t);
//转换为二进制数组 例如 var byte3 = uInt8Array[4]

for(i=0;i<uInt8Array.length;i++){
  d+=String.fromCharCode(uInt8Array[i])
}
</pre>