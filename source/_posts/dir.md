title: __DIR__
tags:
  - PHP
id: 298
categories:
  - PHP Programming
date: 2009-08-07 22:14:56
---

在PHP5.3中，增加了一个新的常量__DIR__，指向当前执行的PHP脚本所在的目录。

例如当前执行的PHP文件为 /www/website/index.php

则__FILE__等于'/www/website/index.php'

而__DIR__等于'/www/website'

现在我们要包含当前文件目录或子目录下的文件，可以直接使用：
<pre lang="php" line="1" file="download.txt" colla="+">
<?php

require_once __DIR__ . '/path/to/test.inc.php';
?>
</pre>

做个笔记。