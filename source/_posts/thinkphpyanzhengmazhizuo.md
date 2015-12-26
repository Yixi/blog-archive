title: ThinkPHP验证码制作
tags:
  - PHP
  - ThinkPHP
  - 技巧
id: 477
categories:
  - PHP Programming
date: 2010-01-04 19:58:31
---

ThinkPHP中的image类中已经集成了验证码的制作，非常的方便。

使用方法如下：
首先在当前控制器中引用验证码：
<pre lang="PHP" line="1" file="download.txt" colla="+">
function verify()
        {
                import('ORG.Util.Image');
                if(isset($_REQUEST['adv']))
                {
                        Image::showAdvVerify();
                }
                else
                {
                        Image::buildImageVerify();
                }
        }
</pre>

这个时候我们就可以在模板中引用验证码了，但为了验证码不过期，我们在模板中加上一个刷新验证码的JS函数。
<pre lang="javascript" line="1" file="download.txt" colla="+">
<script type="text/javascript">
function $(id) {
        return document.getElementById(id);
}
function fleshVerify(){
//重载验证码
var timenow = new Date().getTime();
document.getElementById('verifyImg').src= '__URL__/verify/'+timenow;
}
</script>

<form method="post" name="form1" action="__URL__/writes">
请输入验证码：<input type="text" name="seccode" id="seccode" size="11"  /> 
[![](__URL__/verify/ "如果您无法识别验证码，请点图片更换")](javascript:fleshVerify())
<input type="submit" name="Submit2" value="提交" />
</form>

</pre>

当然最后，我们需要在提交表单内容后对首先对验证码进行判断：
<pre lang="PHP" line="1" file="download.txt" colla="+">
public function writes()
        {
                $seccode=trim($_POST['seccode']);
                if(md5($seccode)!=Session::get('verify'))$this->error('验证码错误!!!');

       ........
}
</pre>

到这里，整个验证码的判断过程就结束了。