

title: title
title: Windows下Graphviz中文乱码解决
date: 2014-05-03 14:14:15
categories:
- 技术点滴
tags:
- tech
- graphviz 
- codec 
- 中文 
- 乱码

---

其实Graphviz本来处理中文就有问题。我存了一个utf8文件(mac下面默认编码），然后到windows下面用Graphviz打开，就乱码。

我把编码改成了gbk，这下windows下面gvedit里面看到的是正确的中文，可是生成的png里面所有中文都是方块乱码。

我上网查了一下，这个[教程](http://blog.csdn.net/xiajian2010/article/details/23748557)很不错。里面提到首先编码就应该是utf8，然后文中应该加上：

	edge [fontname="FangSong"];
	node [shape=box, fontname="FangSong"];

我加了，但是还是有的中文能出来，有的出不来。于是我发觉应该再加上一句：

	graph[fontname="FangSong"];

这下，子图的标题也都是中文正确显示了。可是子图里面的节点却依然是空（不是乱码，只是没有内容）。于是我查找半天，最终发现罪魁祸首是：

	zongshu_title [label = "研究综述" shape=record]

看到了吧？就是最后这句shape=record。为什么有问题？不知道。但是把它删去，一点不改变原先的图形结构，中文却又都出来了。

当然，gvedit是无论如何不能用了。应该使用的是命令行方式，为：

	C:\Users\Administrator>"c:\Program Files\Graphviz2.38\bin\dot.exe" d:\researchPlanSimpleOfficialUTF8.gv -Tpng -o d:\researchPlan.png

好了，这样可以在windows下面正确编译出graphviz文件了。