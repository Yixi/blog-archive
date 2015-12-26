title: ThinkPHP经典普通分页函数以及视图模型。
tags:
  - PHP
  - ThinkPHP
  - 函数
id: 426
categories:
  - PHP Programming
date: 2009-12-23 21:11:30
---

不解释。
<pre lang="PHP" line="1" file="download.txt" colla="+">
//ArticleViewModel.class.php
<?php
class ArticleViewModel extends ViewModel{
  protected $viewModel = true;
  protected $viewFields = array(
  'Article'=>array('id','subject','color','username','postdate','cid','message','content', '_type'=>'LEFT'),
   'Category'=>array('title','_on'=>'Article.cid=Category.id'),
                );
        //protected $viewCondition = array("Article.cid" => array('eqf',"Category.id"));
        public function getPk() {
                return 'id';
        }
}
?>
//========================
//ArticleAction.class.php
<?php
class ArticleAction extends Action{

	public function index(){
		$Article = D('ArticleView');
		$count=$Article->count();
		import("ORG.Util.Page");
		$listRows=15;
		$p= new Page($count,$listRows);
		$list=$Article->limit($p->firstRow.','.$p->listRows)->order('id desc')->findAll();
		$page=$p->show();
		$Category=D('Category')->order("id desc")->findAll();
		$this->assign('cate',$Category);
		if ($list!==false){
			$this->assign('page',$page);
			$this->assign('list',$list);
			$this->assign('count',$count);
			$this->assign('allowbat',$this->allowbat);
		}
		$this->display();
	}
}

?>
</pre>