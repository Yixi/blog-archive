title: js监听text change 事件
tags:
  - HTML5
  - jQuery
id: 843
categories:
  - Firefox
  - javascript
date: 2011-04-23 14:17:10
---

监听输入区域的改变，这里推荐一个jquery的插件：
[http://www.zurb.com/playground/jquery-text-change-custom-event](http://www.zurb.com/playground/jquery-text-change-custom-event)

这个可以监听到内容输入区域内容的实时变化，但是有个小小的不足，就是不能监听到firefox下 设置了contenteditable="true" 的DIV区域的拖拽文字变化。

后来针对firefox下的这种情况写了个简单的处理函数。

<pre lang="javascript" line="1" file="download.txt" colla="+">
<div id="content" contenteditable="true" style="width:500px;height:30px;background:#c1c1c1;"></div>
<script>
    var text="";
    function binchange(){
        var t= $('#content').html();
        if(t!=text){
            console.log('change',text+' to '+t);
            text = t;
        }
        setTimeout('binchange()',3000)
    }
       binchange();
    </script>
</pre>
可以控制settimeout部分的时间参数来控制探测的时间。