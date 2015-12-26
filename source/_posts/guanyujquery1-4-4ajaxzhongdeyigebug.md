title: 关于jquery1.4.4 ajax中的一个BUG
tags:
  - jqeury
id: 764
categories:
  - javascript
date: 2011-01-21 20:15:37
---

在用jquery库的 $.ajax做请求时，当在网络不通（特指断网）的情况下，ajax的返回时会执行success部分的函数。

具体如下：

<pre lang="javascript" line="1" file="download.txt" colla="+">
$.ajax({
    url:url,
    data:{data1:data1,data2:data2},
    type:'POST',
    success:function(data){...},
    error:function(e){....}
});
</pre>

很诡异的是当在无网络的情况执行ajax请求时，会执行success部分的函数。 没试过原生的ajax会有如何的表现。

jquery1.5中对ajax有很大的改变，可以支持通过textstatu来值来指定执行对应函数,像下面：
<pre lang="javascript" line="1" file="download.txt" colla="+">
jQuery.ajax({
    url: 'xxx',
    statusCode: {
        200: function() { 处理请求成功 },
        404: function() { 处理页面未找到 },
        503: function() { 处理Service Unavailable }
    }
});
</pre>

不知道是否能解决上面的情况，待测。