title: 关于ThinkPHP框架前台制作。
tags:
  - PHP
  - ThinkPHP
  - 开发
id: 459
categories:
  - PHP Programming
date: 2009-12-28 21:08:13
---

这几天开始做网站的前台，在这之间倒是走了一个弯路。

因为做后台功能的时候，将数据库中的表和功能对应起来，然后每个表或者功能对应一个控制器，开始做前台的时候就有点犯傻，心想前台每个页面或许会显示不同的表中的内容，但那样怎么来设计控制器呢。

当时还有个犯傻的问题就是纠结在了从数据库中读取文件时，URL路径的表现问题。
<!--more-->
突然想到之前在制作DEDECMS模板的时候，我只是做了一个首页，列表页，文章内容页，突然恍然大悟。

原来自己被做后台时一个功能对应一个Action的思想所禁锢了。

做前台的时候，其实控制器简单多了。比如那样的文章列表，我只需要这样设计就可以了。

三个action，分别是首页，列表也，文章内容页。甚至可以在ThinkPHP中将三个写到一起，三个方法，三个模板。

而且因为没涉及到用户系统，也就是说没涉及到会在前台发生数据添加的问题（除了留言板），甚至可以不用定义模型，直接用M方法进行数据读取。

好了，废话就不多说了，相信和我遇到同一问题的看到这里已经明白怎么回事了。这里贴上我的首页的Action文件。

<pre lang="PHP" line="1" file="download.txt" colla="+">
class IndexAction extends Action{
    public function index(){
        $Announce = M('Announce');
        $Annoulist  =  $Announce->order('id desc')->limit(2)->select(); 

        $Softnew = M('Article');
        $softcid = 'cid=5';   //此处用于对应软件动态栏目的cid值 
        $Softnewlist = $Softnew->where($softcid)->order('id desc')->limit(3)->select();

        $Func = M('Pages');
        $Funcid =6;  //此处用于对应功能演示页面数据ID
        $Funlist = $Func->find($Funcid);

    	$this->assign('annou',$Annoulist);
    	$this->assign('softnew',$Softnewlist);
    	$this->assign('func',$Funlist);
        $this->display();
    }
}
</pre>