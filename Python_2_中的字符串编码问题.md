

title: title
title: Python 2 中的字符串编码问题
date: 2015-09-10 16:19:21
categories:
- 技术点滴
tags: 
- python
- unicode
- ascii
	 
---


都说比起python 3来，2.x版本处理字符串编码有些问题。果然如此。

![](http://7mnmvp.com1.z0.glb.clouddn.com/andysinger_scrabbletiles.png)

（图片来源：[Unicode string detection - Lounge Scene](http://blog.thoward37.me/articles/unicode-string-detection/)）

其实就是默认编码的事情。不管你怎么写，例如开头的

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-  
	

反正它认准了使用ascii了。不信你可以直接这样：

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-  
	
	import sys
	
	print sys.getdefaultencoding()

你猜答案是啥？

	➜  wsyMarkdownTools git:(master) python test_codecs.py            ±[A1][master]
	ascii
	

是不是能把活人气死啊？

这样一来，就有许多问题需要处理了。例如说`json.load()`或者`json.loads()`函数，那么默认生成的一个字典就是utf-8编码的。

你可以正常读取它，但是获得的内容可都是`u'string'`这种类型的。如果你打算把它拷贝进入剪贴板……那可就要报错了。

	UnicodeDecodeError: 'ascii' codec can't decode byte 0xe7 in position 10: ordinal not in range(128)

一开始我真的不知道该怎么办了，最后甚至使用`reload(sys)`这种笨办法。

后来发现了[这篇教程](http://www.jb51.net/article/17560.htm)，立刻有了灵感。

当我们遇到这种特殊问题的时候，还是得向着ascii靠拢，所以可以在读取了json之后，查字典完成的时候，获得某个字符串（是unicode的哟），后面紧接着跟一个encode()函数，强制转换。

例如在我的`mdImageLinkHandler.py`脚本中出现的：

	prefix = prefix_settings[prefix_type].encode('gb2312')

