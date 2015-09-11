

title: title
title: nbconvert的使用
date: 2013-10-07 20:29:25
categories:
- 技术点滴
tags:
- 格式转换
- python
- 科研
---

ipython notebook很好用，但是只有安装了ipython环境的计算机才能打开并且浏览、操作ipynb格式的文件。科研流程需要发布共享给其他科研工作者，因此必须采用更为通用的格式。幸好，ipython提供了转换器nbconvert，可以将ipynb格式转换为html、latex和markdown等纯文本通用格式，以便使用不同类型、不同版本操作系统的读者都可以打开该文件，查看其内容，甚至拷贝其代码在本地运行。

nbconvert的使用方法如下：

\`\`\`
	$ipython nbconvert --to html example.ipynb
	[NbConvertApp] Using existing profile dir: u'/Users/Apple/.ipython/profile_default'
	[NbConvertApp] Converting notebook example.ipynb to html
	[NbConvertApp] Support files will be in example_files/
	[NbConvertApp] Loaded template html_full.tpl
	[NbConvertApp] Writing 406527 bytes to example.html
\`\`\`

获得的结果如图所示。