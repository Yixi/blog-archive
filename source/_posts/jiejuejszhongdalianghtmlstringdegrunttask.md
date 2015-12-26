title: 解决js中大量HTML string的grunt task
tags:
  - grunt
  - nodejs
id: 1122
categories:
  - javascript
date: 2013-10-13 10:03:09
---

前面一段时间在继续深入优化diigo流程时，遇到了需要在js中写入大量HTML来作为ajax完成后的处理。

内容短的html直接写入js中还算合适，但随着html越长，便开始难于阅读和维护，即使像webstorm对HTML string有较好的书写支持，但仍不够。

后来想到以前diigolet的项目中，也有同样的问题，diigolet那边的做法是将所有的html写到一个template.html文件中，用注释表明变量模块，然后最终在build时使用rakefile来把html文件中的块读出并合并到js文件中作为一个string变量。

现在有grunt，理论可以用node更简单的做这样一件事情，便花了一天时间写出了一个grunt task。

[https://github.com/Yixi/grunt-YHtmlToJs](https://github.com/Yixi/grunt-YHtmlToJs)

在package.json中加上依赖:
<pre lang="javascript" line="1" file="download.txt" colla="+">
...
"y-html-2-js":"latest"
...
</pre>
然后
<pre lang="shell" line="1" file="download.txt" colla="+">
npm install
</pre>
详细用法参考github readme