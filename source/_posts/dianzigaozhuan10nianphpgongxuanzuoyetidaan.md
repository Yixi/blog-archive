title: 电子高专2010学年PHP公选作业题答案
tags:
  - PHP
  - 电子高专
id: 604
categories:
  - PHP Programming
date: 2010-06-03 22:13:20
---

下面依次是第3题，第4题，第5题的完全PHP代码。

高专有需求的直接拿了 不解释了。

第3题
这道题其实比较蛋疼，因为第一个提交和第二个汇总要求都要显示出前面的提交过的数据，所以不能当成两个表单来弄，需要重叠一次表单区域。
<pre lang="PHP" line="1" file="download.txt" colla="+">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>第3题解答</title>
</head>
<body align="center">
    <form name="form1" method="post" action="">

请输入班级学生人数
        <input type="text" name="num"  value="<?=isset($_POST['num'])?$_POST['num']:""?>" />
        <input type="submit" name="button_a"  value="提交" />

    <?php
        if(isset($_POST['button_a'])){
            $num = $_POST['num'];
            for($i=1;$i<=$num;$i++){
                echo "第$i 个学生的成绩";
                echo "<input type=\"text\" name=\"stu$i\" />"."
";
            }
            echo "<input type=\"submit\" name=\"button_b\"  value=\"汇总成绩\" />";
        }

        if(isset($_POST['button_b'])){
            $num=$_POST['num'];
            $totle=0;
            for($i=1;$i<=$num;$i++){
                echo "第$i 个学生的成绩";
                $s=isset($_POST['stu'.$i])?$_POST['stu'.$i]:"";
                echo "<input type=\"text\" name=\"stu$i\" value=\"$s\" />"."
";
                $totle+=$s;
            }
            echo "<input type=\"submit\" name=\"button_b\"  value=\"汇总成绩\" />"."

"; 
            echo "总成绩为 : $totle";
        }
    ?>
</form>
</body>
</html>
</pre>
<!--more-->
第4题
难度不大，一个数组排序函数解决
<pre lang="PHP" line="1" file="download.txt" colla="+">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>第4题解答</title>
</head>
<body>
    请输入需要排序的数据

    <form name="form1" method="post" action="">
        <input type="text" name="a" value="<?=isset($_POST['a'])?$_POST['a']:""?>" />-
        <input type="text" name="b" value="<?=isset($_POST['b'])?$_POST['b']:""?>" />-
        <input type="text" name="c" value="<?=isset($_POST['c'])?$_POST['c']:""?>" />-
        <input type="text" name="d" value="<?=isset($_POST['d'])?$_POST['d']:""?>" />-
        <input type="text" name="e" value="<?=isset($_POST['e'])?$_POST['e']:""?>" />- 
        <input type="submit" name="button"  value="提交" />   
    </form>  
<?php
    if(isset($_POST['button'])){
        $arr=array($_POST['a'],$_POST['b'],$_POST['c'],$_POST['d'],$_POST['e']);
        sort($arr);
        echo "排序后的数据如下所示： 
";
        foreach($arr as $key => $val){
            echo $val."
";
        }
    }
?>
</body>
</html>
</pre>
第5题
知道求星期几的函数后就很好解决了。
<pre lang="PHP" line="1" file="download.txt" colla="+">
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>第5题解答</title>
</head>
<body>
<form name="form1" method="post" action="">
  请输入您的出生日期
  <input type="text" name="year"  value="<?=isset($_POST['year'])?$_POST['year']:""?>"/> 
  年
  <input type="text" name="mon"  value="<?=isset($_POST['mon'])?$_POST['mon']:""?>"/> 
  月
  <input type="text" name="mday" value="<?=isset($_POST['mday'])?$_POST['mday']:""?>"/>
  日
  <input type="submit" name="button"  value="提交" />
</form>

<?php
    if(isset($_POST['button'])){ 
    $dateold = ($_POST['year']."-".$_POST['mon']."-".$_POST['mday']);
    $date = date("Y-m-d") ;
    $age = $date-$dateold;

    $d=date ("l", mktime (0,0,0,$_POST['mon'],$_POST['mday'],$_POST['year']));
    echo "
";
    echo "您的年龄为：{$age}
";
    echo "出生时是一周的：{$d}";
}
?>
</body>
</html>
</pre>