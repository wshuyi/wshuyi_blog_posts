

title: title
title: PyCX 一个纯python编写的ABM软件
date: 2015-01-15 22:10:48
categories:
- 技术点滴
tags: 
- python
- pycx
- abm
	 
---




上午用udacity学了会儿python，真是觉得感觉又回来了。想想后面又得用netlogo，心里就不是太爽。再次搜索一下netlogo python。虽然还是没啥新东西，不过突然找到了这篇blog[python | simulatingcomplexity](https://simulatingcomplexity.wordpress.com/tag/python/)，里面推荐了[SourceForge.net: PyCX Project](http://pycx.sourceforge.net/)，让人感觉豁然开朗。

![](http://7mnmvp.com1.z0.glb.clouddn.com/pycxFrontpage.jpg)


这东西最吸引我的地方在于它并不是一个什么abm软件，而是一个python库。也就是你可以直接运行上面的各种示例model，不需要按照任何新的东西。当然，这是在你安装了anaconda的情况下。 :-P

不过，我试着从shell里面直接运行 python xxx.py ，遇到问题。只有设置界面出来了。运行界面（就是上面各种图形的那个）出不来。尝试ipn运行，也不行。

不过后来看到一个介绍，说不要在ipython里面用pylab，而我的ipn里面是pylab --inline的。

![](http://7mnmvp.com1.z0.glb.clouddn.com/pycxNote2UserEnthoughtAnaconda.jpg)


于是干脆进入 pycx3.1的目录，执行ipython notebook，进入之后直接用magic command，执行


	%run xxx.py


![](http://7mnmvp.com1.z0.glb.clouddn.com/pycxRunScript.jpg)


所有该出现的界面就都出来了，非常好用。

如果我打算看看文件的内容都有哪些，也可以用magic command。


	%load xxx.py


![](http://7mnmvp.com1.z0.glb.clouddn.com/pycxLoadScript.jpg)

PyCX的作者已经很长时间将该款软件应用于教学和科研，取得了不错的成果。

![](http://7mnmvp.com1.z0.glb.clouddn.com/pycxUserRating.jpg)

作者还写了一篇论文描述为啥弄这个python版的ABM[Complex Adaptive Systems Modeling | Full text | PyCX: a Python-based simulation code repository for complex systems education](http://www.casmodeling.com/content/1/1/2)，还有个slides[pycx.sourceforge.net/PyCX-ECAL2013-tutorial.pdf](http://pycx.sourceforge.net/PyCX-ECAL2013-tutorial.pdf)，很有意思。
