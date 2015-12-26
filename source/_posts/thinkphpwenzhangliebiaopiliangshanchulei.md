title: ThinkPHP文章列表批量删除类。
tags:
  - ThinkPHP
  - 开发
id: 419
categories:
  - PHP Programming
date: 2009-12-22 11:24:29
---

在模板中使用
> &lt;input name="id[]" type="checkbox" id="id[]" value="{$vo.id}"&gt;

此类基于ThinkPHP 最新版2.0写出，其他版本未与测试。

此方法可以写于GlobalAction.class.php中，此类继承ThinkPHP的Action类，其他控制器继承 GlobalAction类。
<pre lang="PHP" line="1" file="download.txt" colla="+">
class GlobalAction extends Action{

	public function _subAction($dbclass=""){
		$getid=$_REQUEST['id'];  //获取ID
		if (!$getid) $this->error('未选择记录');
		$getids=implode(',',$getid);
		$id = is_array($getid)?$getids:$getid;
		$act =$_REQUEST['act'];
		if (!$act) $this->error('操作类型必须选择');
		$allowact=array('delete');   //此处用来判断操作的方式，可加入更多的判断用于公共类
		if(!in_array($act,$allowact)) $this->error('未知操作');
		if (!$id) $this->error('ID丢失');
		$dbname=$this->getActionName();  //获取当前控制器，用于对应数据表。

		switch ($act){
			case 'delete':$Result=D($dbname)->execute('DELETE FROM __TABLE__ where `id` IN ('.$id.')');$say='删除成功';;break;//删除

		}
		if($Result==false){
			echo $this->n;

		}else{
			$this->assign('jumpUrl',__URL__/$dbname);
			$this->success($say);
		}
	}

}
</pre>