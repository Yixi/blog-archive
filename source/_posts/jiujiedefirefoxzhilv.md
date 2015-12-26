title: 纠结的firefox之旅
tags:
  - Add-on
  - firefox
  - jetpack
id: 882
categories:
  - Firefox
date: 2011-05-23 21:32:00
---

从firefox4发布之前开始使用jetpack来开发firefox add-on到现在已经有几个月的时间，在最初移植chrome的Quick Note和Read Later Fast时，在传统的XUL方式和新的jetpack开发之间选择了jetpack，原因有下几点：

1，传统的XUL开发add-on的方式打开资源页面是为chrome://的前缀，而这个前缀不能使用indexdDB来储存数据。
2，新的jetpack方式比较易上手。
3，以为使用jetpack这个mozilla比较推荐的SDK开发出的ADD-on会在firefox4发布时的那个评选10个优秀插件会有更高的权重。

随着另一个同事负责的一个新的firefox add-on的项目开发，那位同事对firefox的插件的开发经验很丰富，diigo历来的firefox toolbar就是他开发的，这个新项目和Read Later Fast和Quick Note的需求很近，单页面，本地储存数据。

他没有使用jetpack来开发，依然使用传统的XUL的创建方法，通过一些方法自己创建了一个resouce://的页面来使用本地储存indexdDB技术。

想想我们之前可能是因为firefox4要发布，时间压力很大，所以没研究透就使用jetpack来开发。随着后续开发的需求越来越多，才发现jetpack很难完成我们需要的需求。

比如说就那个简单的定义button，用传统的XUL的方式就是那么几个XUL标签，但在jetpack中实现起来需要写很长的一段代码来实现（这个方法我在前面的博文提到过）。

就像现在Firefox版本的Quick Note中，作为jetpack的lib库下编写的JS中，一共有530行左右代码，其中大概有150行的功能是实现ajax请求中转和contentscript与add-on proccess通信，其余的近400行代码都是在定义UI上，主要就是右上角的button和sidebar。而这个UI 如果用XUL的方式来做的话，大概就是近10行左右的xul标签就能实现。而且因为一些必须要的需求，不得不去写重复的代码，因为XPCOM中调用的方法无法直接使用我main.js中的方法。

因为大部分都是使用jetpack来调用XPCOM部分来操作，且通过动态插入document的方法来自定义化UI，会产生什么样的副作用或者BUG，现在还未知，虽然已经解决了很多已知的问题，比如disable插件，自定义添加的UI不消失等问题。

现在回想起来，当初应该更深入的了解firefox add-on的开发机制，而应该选用传统的XUL的方式来开发。
而对于jetpack，真的看不出有什么能让开发者都去使用的特点。仅仅是上手容易？但限制太高。

但现在已经使用了jetpack的方式来开发，只能一条路走到黑。

不过这折腾的写法，也算是走在最前沿了。