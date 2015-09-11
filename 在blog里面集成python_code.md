

title: title
title: 在blog里面集成python code
date: 2015-01-17 11:34:27
categories:
- 技术点滴
tags:
- blog
- python

---

其实我对于ipython notebook已经非常满意了。更加上后来学会了如何配置vim直接f5执行一段python code之后，本来觉得不会再去碰什么网页python版本了。那东西好像都是为了纯教学的目的。

可是由于在udacity的课程里面需要我绘制turtle。这里立刻就体现mac下面python turtle的问题了。一执行就会跑出来一个终端窗口，叫做python。这本来没有什么。可是这个终端窗口每次出来都在一堆窗口的下方。等你用鼠标把它点到前台来看的时候。上面所有的动画动作就都已经做完了……

我尝试了若干种解决办法，用了好几个小时的时间，也没有能够搞定。我这个人还真不是一个非常灵活的人。这个坎儿就导致我根本没有办法进一步往下学习课程了。

尝试了idle, ipython, vim, ipython notebook。翻遍了网上各种论坛里面的蛛丝马迹。却没有一个好的解决方法。

突然在一个论坛里面，有人提议真正跨平台的方法是使用网页版python。我于是尝试一下，从[Skulpt](http://www.skulpt.org/)很快进化到了[Trinket helps you teach with code](https://trinket.io/home)。

一开始只是因为它上面的说明更详细，而且可以支持多个文件（这样就不必把所有的module都拷贝到一个主文件下面了）才使用。后来才发现，这东西简直就是给教育工作者量身打造的神器。根本就不用下载任何东西。打开就可以输入代码执行演示。

而且，具有方便的代码内嵌功能。例如下面这一段：


	<iframe src="https://trinket.io/embed/python/32d416c6d4" width="100%" height="400" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen>
	</iframe>


就能出现下面这个界面了。点一下其中的运行按钮，看看能出现什么？ :-P

<iframe src="https://trinket.io/embed/python/32d416c6d4" width="100%" height="400" frameborder="0" marginwidth="0" marginheight="0" allowfullscreen></iframe>

这样以后如果需要教python，可以非常自豪地跟机房老师说：“把网联上就可以了，您啥都不用安装。”