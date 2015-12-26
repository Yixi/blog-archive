title: 给个PHP分页函式。
tags:
  - PHP
  - 函数
id: 205
categories:
  - PHP Programming
  - 工作记录
date: 2009-06-21 18:47:11
---

今天比较累，就不做过多的说明了。函式在下面。
先给个简短的说明吧：
/*
#### 检索分页函式 ####
Int $HALT - 检索结果仅分1页时是否(1/0)显示页码条
Int $LRLIST - (页码条显示页码数-1)/2
Int $ECHOCNT - 检索时每页显示记录的数量
Int $paper - 页数，预提取：$paper=$HTTP_GET_VARS[paper];
Varchar $table - 数据表名,预附值：$table="db.table";
Varchar $where - 检索条件，预附值：$where="where field='value'";

Varchar $enwhere - 将原$where进行两次base64_encode()编码后以GET的方式提交
Varchar $splitstr - 页码条输出字串，执行函式后在相应的位置执行 echo $splitstr;

函式调用前需获取变量 - 
$paper=$HTTP_GET_VARS[paper];
$sumcnt=$HTTP_GET_VARS[sumcnt];
$enwhere=$HTTP_GET_VARS[enwhere];

Return (Varchar $where) - 分页后检索语句的检索条件
注意：本函式需调用出错处理函式 nerror($error);
*/

[sourcecode language='php']<?

function splitlist($HALT,$LRLIST,$ECHOCNT,$paper,$table,$where,$page_id,$userid){ 
global $splitstr,$sumcnt;
if($paper=="" || $sumcnt==""){ 
$query = "select count(*) as num from $table $where";
$result = mysql_query($query);
$row = mysql_fetch_array($result);
$sumcnt=$row["num"];
if($sumcnt==0){ 
nerror("该版内还没有选择发布新闻 ！");
}
$paper=1;
}
$sumpaper=($sumcnt-$sumcnt%$ECHOCNT)/$ECHOCNT;
if(($sumcnt%$ECHOCNT)!=0) $sumpaper+=1;
if($sumpaper==1 &amp;&amp; $HALT==0) return($where);
$enwhere=base64_encode(base64_encode($where));
if(($LRLIST*2+1) < $sumpaper){ 
if(($paper-$LRLIST) < 2){ 
$tract=1;
$sub=$LRLIST*2+1;
}else if(($paper+$LRLIST) >= $sumpaper){ 
$tract=$sumpaper-($LRLIST*2);
$sub=$sumpaper;
}else{ 
$tract=$paper-$LRLIST;
$sub=$paper+$LRLIST;
}
}else{ 
$tract=1;
$sub=$sumpaper;
}
$uppaper=$paper-1;
$downpaper=$paper+1;
$startcnt=($paper-1)*$ECHOCNT;
$where.=" limit ${ startcnt },${ ECHOCNT }";
if($tract > 1) { $splitstr="【 << "; } 
else $splitstr="【 << ";
for($i=$tract;$i<=$sub;$i++){ 
if ($i!=$paper) $splitstr.="".$i." ";
else $splitstr.="".$i." ";
}
if ($sub!=$sumpaper) $splitstr.=">> 】";
else $splitstr.=">> 】";
return($where);
}
?>
[/sourcecode]