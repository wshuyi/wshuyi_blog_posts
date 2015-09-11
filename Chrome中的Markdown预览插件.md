

title: title
title: Chrome中的Markdown预览插件
date: 2014-11-10 21:48:15
categories:
- 技术点滴
tags:
- chrome
- markdown

---


虽然有了马克飞象，但我还是觉得啥东西都放在里面并不好，因为同步确实比较花费空间，尤其是本来照片已经在dropbox里面了，同步到Evernote中，然后觉得还是进Dayone比较好。那不就全都浪费了？Evernote可是按照流量算啊。

而且使用马克飞象，并不能真正让我获得vim的编辑性能。虽然它也提供了一个vim操作模式，但是地球人都知道vim哪里是一个网页版编辑器可以替代的？

但是，我既然打算使用Vim，又实时需要观察结果，那么恐怕有个东西就必不可少了，那就是Markdown Preview Plus，Chrome的一个插件了。

安装之后，这个选项一定要勾选。

![](http://7mnmvp.com1.z0.glb.clouddn.com/markdownPreviewSetting1.png)

然后就是选择一下同步更新的周期。我觉得3秒钟是个可以接受的时间。

![](http://7mnmvp.com1.z0.glb.clouddn.com/MarkDown_Preview_Plus_options2.png)

但是出来的效果未必好。因为其他选项情况下，图片可能非常大。而github里面，图片虽然正常了，字体却又太小。我于是在整个系统里面找css。发现sublime text2下面有个github.css，于是又按图索骥找到了其中的一个markdown.css，用起来觉得效果还行。

![](http://7mnmvp.com1.z0.glb.clouddn.com/markdownPreviewPluscss.png)