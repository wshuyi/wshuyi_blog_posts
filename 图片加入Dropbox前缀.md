

title: title
title: 图片加入Dropbox前缀
date: 2015-08-02 16:22:02
categories:
- 技术点滴
tags:
- dropbox


---

## 前言

打算把自己的写作主要编辑器转移到Ulysses，可是里面插入图片却遇到了一个问题，那就是插入的图片都成了本地路径，没有任何前缀路径。对于我来说，这也不是什么大问题。因为我用Dropbox做图床。只需要在前面加一个路径名称就可以了。这里编写一个脚本，从剪贴板里面读取markdown源文件，然后找到每一行包含图片路径的语句，把其中的本地本目录路径加上一个Dropbox前缀。

## Python脚本编写

这里突然想到，一直不敢发布我的Markdown工具集，是因为怕暴露自己的Dropbox前缀路径等私有信息。今天干脆一鼓作气，把这个问题解决了好了。其实也没啥，只需要专门弄一个py文件（不需要加密，只要放到.gitignore就可以），存储几个变量名称。需要的时候import一下即可设置这些基本信息。

	try:
	    from user_private_settings import *
	except:
	    print """'user_private_settings.py' not found. \nYou need to specify the dropbox_link_prefix and qiniu_link_prefix"""
	    exit(1)


整体的python脚本mdImageAddDropboxPrefix.py如下：

	#!/usr/bin/env python
	# -*- coding: utf-8 -*-  
	
	import wsyFileOperator
	try:
	    # user_private_settings.py is the place to store some user specific paths or tokens
	    # We 'll try to import this python file
	    from user_private_settings import *
	except:
	    # If there is something wrong, means that you cloned this file from git repository
	    # However, the user_private_settings.py was not cloned for privacy reason
	    print """'user_private_settings.py' not found. \nYou need to specify the dropbox_link_prefix and qiniu_link_prefix"""
	    exit(1)
	
	def add_image_dropbox_prefix_line(line, dropbox_link_prefix):
	    # In markdown image link start with '![](http://7mnmvp.com1.z0.glb.clouddn.com/'
	    markdown_image_start_str = '![](http://7mnmvp.com1.z0.glb.clouddn.com/'
	    if line.find(markdown_image_start_str) >= 0:
	        line = line.replace(markdown_image_start_str, markdown_image_start_str + dropbox_link_prefix)
	    return line
	
	def add_image_dropbox_prefix_cpb2cpb(dropbox_link_prefix):
	    # We need to split the content from clipboard into separate lines
	    data = wsyFileOperator.getClipboardData().split('\n')
	    # And after handling with the lines, we need to join them together
	    new_data = '\n'.join([add_image_dropbox_prefix_line(line, dropbox_link_prefix) for line in data])
	    # Push back the content to clipboard again
	    wsyFileOperator.setClipboardData(new_data)
	
	# When loading this script, we would like to run this function.
	add_image_dropbox_prefix_cpb2cpb(dropbox_link_prefix)
 
 
 
 

问题在于，每次我都需要把内容拷贝到剪贴板，然后再跑到终端下面，执行mdImageAddDropboxPrefix.py，然后再操作。这里在终端下面执行命令让我感觉不好。怎么办？

## Alfred尝试

我的解决方法是利用alfred。

Alfred可以通过Alt+Space轻易呼唤应用程序。可惜，python脚本不能算作是应用程序。因此，即使你把wsyMarkdownTools目录加入到Alfred的搜索路径，依然不能查找执行python脚本。

## Automator外壳

解决途径是再绕一下，在python脚本外面加个壳儿。

壳儿是什么？是Automator。

![](http://7mnmvp.com1.z0.glb.clouddn.com/automatorNewDocumentSelectType20150802.jpg)

Automator新建一个应用程序，然后选择动作类型为“运行shell脚本”，填入如下图的语句。

保存在iCloud的Automator默认文件夹下面，名称为dropboxPrefixAddtoUlyssesMarkdownImageLinks。

![](http://7mnmvp.com1.z0.glb.clouddn.com/automatorAppOverPythonScript20150802.jpg)

且慢，现在Alfred里面依然是找不到这个应用程序，因为该路径没有在Alfred的搜索路径列表里面。

![](http://7mnmvp.com1.z0.glb.clouddn.com/alfredFeatureSettingSearPath20150802.jpg)