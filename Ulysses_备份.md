

title: title
title: Ulysses 备份
date: 2015-08-06 22:28:19
categories:
- 技术点滴
tags: 
 
---

在网上寻找到了一个python调用zip备份的样例：

## 利用python压缩一个文件夹

	#!/usr/bin/env python
	import os
	import zipfile
	
	def zipdir(path, ziph):
	    # ziph is zipfile handle
	    for root, dirs, files in os.walk(path):
	        for file in files:
	            ziph.write(os.path.join(root, file))
	
	if __name__ == '__main__':
	    zipf = zipfile.ZipFile('Python.zip', 'w')
	    zipdir('tmp/', zipf)
	    zipf.close()
下面我们来自己测试一下zipfile模块吧

## zipfile 测试

在python里面，我们使用zipfile来进行文件的压缩。

为了测试多文件夹、文件夹里面含有空格等问题。我们做了一个测试。

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-  
	
	import os
	import zipfile
	
	def zipdir(path, ziph):
	    # ziph is zipfile handle
	    for root, dirs, files in os.walk(path):
	        for file in files:
	            ziph.write(os.path.join(root, file))
	
	
	dir1 = os.path.expanduser('~/Downloads/testZipdir/testa')
	dir2 = os.path.expanduser('~/Downloads/testZipdir/testb')
	dir3 = os.path.expanduser('~/Downloads/testZipdir/test c')
	target_zipfile = os.path.expanduser('~/Documents/python_zipfile_test.zip')
	zipf = zipfile.ZipFile(target_zipfile, 'w')
	zipdir(dir1, zipf)
	zipdir(dir2, zipf)
	zipdir(dir3, zipf)
	zipf.close()

经测试，多文件夹、空格都可以正确应对，很好。

但是每一次都这样输入多个文件夹，步骤多比较麻烦。也做成函数好了。 :-P

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-  
	
	import os
	import zipfile
	
	def zip1dir(path, ziph):
	    # ziph is zipfile handle
	    for root, dirs, files in os.walk(path):
	        for file in files:
	            ziph.write(os.path.join(root, file))
	            
	
	            
	def zipdirs(paths, target_zipfile):
	    zipf = zipfile.ZipFile(target_zipfile, 'w')
	    for path in paths:
	        zip1dir(path, zipf)
	    zipf.close()
	    
	dir1 = os.path.expanduser('~/Downloads/testZipdir/testa')
	dir2 = os.path.expanduser('~/Downloads/testZipdir/testb')
	dir3 = os.path.expanduser('~/Downloads/testZipdir/test c')
	target_zipfile = os.path.expanduser('~/Documents/python_zipfile_test.zip')
	paths = [dir1, dir2, dir3]
	
	zipdirs(paths, target_zipfile)

## 实际制作Ulysses备份zip文件

那么下一步，我们把单文件夹压缩和多文件夹压缩都做到我们的wsyFileOperator.py 里面。然后这次我们要实际操作了。

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-  
	
	import os
	import wsyFileOperator
	    
	dir1 = os.path.expanduser('~/Library/Mobile Documents/X5AZV975AG~com~soulmen~ulysses3')
	dir2 = os.path.expanduser('~/Library/Mobile Documents/X5AZV975AG~com~soulmen~dtouch')
	
	target_zipfile = os.path.expanduser('~/Documents/ulysses_dtouch_documents_backup.zip')
	paths = [dir1, dir2]
	
	wsyFileOperator.zipdirs(paths, target_zipfile)

很简洁，是不是？其实有一处我没有弄懂。就是明明wsyFileOperator.py里面已经包括了`import os`，为何这里我还得再次输入一遍呢？

如果wsyFileOperator.py里的import不作数，那么`import zipfile`又该如何解释呢？不知道。

## 空文件夹的处理

空文件夹是不被包含在压缩包里面的，这应该是一个不该发生的故事。

不过对于文件备份来说，其实也有道理。毕竟嘛，里面没有文件，你让我备份啥？不过对于来说保持目录结构的完整性来说，还是很有必要的。



## 定时执行

开始以为这是个很困难的事情。后来才发现，原来osx下面的automator如此强大。

新建automator文稿的时候，就有日历提醒这一项。

![](http://7mnmvp.com1.z0.glb.clouddn.com/20150806_155609_snapshot_01.jpg)

只接受日历事件作为输入。我依然拖了一个shell进来，里面填写的脚本当然就是我前面写的python脚本喽。

	/Users/wsy/Dropbox/var/wsywork/wsoft/wsyMarkdownTools/ulyssesDocumentsBackup.py

![](http://7mnmvp.com1.z0.glb.clouddn.com/20150806_155534_snapshot_01.jpg)

存储的时候会自动打开日历应用，只需要设置事件，以及是否重复就可以了。我设定为每天晚上9点半进行备份。

![](http://7mnmvp.com1.z0.glb.clouddn.com/20150806_154504_snapshot_01.jpg)

注意其中“打开文件”几个字很重要。只有设置了它才会真正执行脚本。
