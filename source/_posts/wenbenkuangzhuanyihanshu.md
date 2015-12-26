title: 文本框转义函数。
tags:
  - PHP
  - 函数
id: 473
categories:
  - PHP Programming
date: 2010-01-03 17:47:45
---

我怎么总觉得好像标题打错了。。

<pre lang="PHP" line="1" file="download.txt" colla="+">
function dhtml($string) {
  if(is_array($string)) {
    foreach($string as $key => $val) {
	$string[$key] = dhtml($val);
	   }
    } else {
    $string = str_replace(array('"', '\'', '<', '>', "\t", "\r", '{', '}'), array('&quot;', '&#39;', '&lt;', '&gt;', '&nbsp;&nbsp;', '', '&#123;', '&#125;'), $string);
	}
	return $string;
    }

</pre>