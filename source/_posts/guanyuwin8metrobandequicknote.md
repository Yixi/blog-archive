title: 关于win8 metro版的Quick Note
tags:
  - CSS
  - javascript
  - metro
  - win8
id: 1033
categories:
  - javascript
  - win8
  - 工作记录
date: 2012-01-10 00:16:24
---

随着US时间1月8号M$第一波参赛程序的提交截止，Quick Note for Win8的开发也算是告一段落，中间因为一些各种准备不充分问题，虽然这次提交的版本还没达到最完美的我想要的最完美的状态，但总算顺利的完成任务。

这之间有很多波折，从最早的win8 developer preview发布时，我曾第一时间在我的笔记本上直接硬盘安装win8，大概的了解了metro界面和以前传统desktop的区别，并简单的从visual studio 11 preview中创建了一个split的javascript metro项目，build，整个过程很顺利，简单的浏览了项目文件的组成，当时评估是基于web的APP很好移植，甚至你可以简单的理解成使用javascript build的metro程序其实就是封装了一个全屏的IE10而已（现在开来，这句话理解也确实没有错）。

凭着这个了解，粗略的评估了quick note应该是比较容易移植到win8 metro下，而因为preview中的win8 app store并没有开放，当时得到的消息是今年的2月份开放，所以这事情搁置了一旁，然后投入到另一个项目的开发中。

然后上个月下旬的时候得到一个消息说，M$在5个国家地区（不包括CN）有个第一波提交metro app的评选，将会出现在win8 beta版本的store中预置，这是个绝好的先机，所以迅速将重心转移到这边。

首先要思考的第一个问题是quick note数据的存放问题，因为考虑之前偶尔会有用户抱quick note chrome版本数据丢失的问题，所以这次想找个比较稳妥的数据储存模式，在了解懂啊winRT并没有提供SQL的数据库支持，并在一些第三方的选择比如winrtsql等，最后还是选择了使用html5中的indexdb，第一，这是metro中唯一有文档的数据库级别的储存，第二，之前在firefox中的quick note也是使用indexdb储存，移植应该会很顺利。

然后是文件的迁移，并解决一些列bug，以及一些IE10的兼容问题，以及一些metro app的一些特殊兼容问题，比如不允许直接使用innerHTML之类的方法（当然也包括jquery的.html()方法），debug，竟然出奇的顺利，两天时间就能把chrome的quick note移植到win8中，并还有和diigo的云同步功能。

事情转变在某天晚上看了win8 build大会的视频后，重新认识了metro UI的设计。

因比赛的评分使用metro UI的分值比重是50%，看了视频后，直接推翻直接准备在基于split view的模板上重新设计quick note。

和UI nancy简单的讨论后，然后开始迅速的搭建HTML结构原型。

并尽量的去使用metro winJS中提供的UI，比如app bar ,setting ,listview之类的东西。

后来又添加上了系统层的share，search之类的东西。

因为时间问题，中间取舍了很多，最后提交的版本中，里面有个indexdb的小bug也未来得及解决，只是用了一些hack的办法去处理（关于什么bug，和firefox中indexdb的区别，我后面会专门开文章介绍）。

虽然赶在了截止之前提交了程序，但是是否能入围，只能祈祷。我自己做出来的东西，我只能打70分，如果给我更充裕的时间，我能研究透win8的API，应该能把quick note做的更完善。

祈祷能入围吧。

![](http://blog.liuyixi.com/wp-content/uploads/2012/01/win8.png "win8")