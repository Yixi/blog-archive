title: JSON数组排序
tags:
  - JSON
  - 函数
id: 796
categories:
  - javascript
date: 2011-03-03 12:57:25
---

因最近折腾indexedDB需要，所以有了这个函数。
需求：根据数组中JSON某个字段值来排序输出数组。

<pre lang="javascript" line="1" file="download.txt" colla="+">
var sort_by = function(field, reverse, primer){ 
				reverse = (reverse) ? -1 : 1; 
				return function(a,b){ 
				    a = a[field]; 
				    b = b[field]; 
				    if (typeof(primer) != 'undefined'){ 
					a = primer(a); 
					b = primer(b); 
				    } 
				    if (a<b) return reverse * -1; 
				    if (a>b) return reverse * 1; 
				    return 0; 
				} 
			}
</pre>

用法：

例如有这么一个JSON:

<pre lang="javascript" line="1" file="download.txt" colla="+">
var items = [
{name:'a',sort:5},
{name:'b',sort:7},
{name:'d',sort:1},
{name:'c',sort:3}
]

//按sort的大小来排序数组
items.sort(sort_by('sort',false,parseInt));

</pre>