

title: title
title: 将dayone中的markdown转换为hexo源文件格式
date: 2014-08-24 16:13:09
categories:
- 技术点滴
tags:
- dayone
- markdown
- hexo

---


## 缘起

日记坚持得还算可以，可是blog已经可以用“田园荒芜”来形容了。最近重新启用了hexo，在github和gitcafe上面同步部署。有了发布内容的渠道。但是我之前写的许多文章目前都在dayone里面。大多已经利用各种脚本转变为了dayone特有的markdown格式。这里面题目一般用一级标题来显示，正文中最高级别是二级标题。标签用"\#<tag>"来表示。日期不在正文里面，由dayone自己加入元数据填充搞定。

正因为每次往hexo里面导入之前写作的文章都需要进行转换，因此没有什么动力，觉得麻烦。每次都需要hexo init <filename>，然后跑到

> source/\_posts

这个文件夹里面找到自己新生成的文章。打开后里面一般有3行文字：

> title: Title of this article
> date: xxxx-xx-xx xx:xx:xx
> tags:


需要手动把dayone里面的tag转化成这里的格式，即"# <tag>"变成"- <tag>"填到"tags:"下方。正文里面去掉title，把所有标题级别上提一个等级……

想想都觉得麻烦。

于是今天的目标在于，把上述工作全都自动化。之前比较纠结的一点在于——从哪里开始。当然可以在vim或者emacs编辑器里面开始用宏来做一些工作。但是局限性比较大。尤其是我现在emacs和vim基本上都处于半吊子水平。从python开始，自然比较好。可是每次还得指定某个文件名，真麻烦。尤其是大部分数据都在dayone里面。每次拷贝粘贴到某一个文件。再转入命令行下面去调用python执行脚本处理某个指定的文件名，也不是多么好的解决方法。

但是早上突然灵光一现——拷贝粘贴不是要用剪贴板吗？那我直接从剪贴板开始不就得了？于是就从零开始编了一个脚本。首先自然要在ipython notebook里面开始，试着执行没问题了，调整了顺序后，导出为py文件，就形成了现在用的这个脚本

> blogDayone2Hexo.py

## 使用方法

dayone中找到某篇日志，edit点击编辑。内容修改完成后全文复制到剪贴板。

进入自己的hexo日记文件夹。

确认blogDayone2Hexo.py权限为可执行，并且已经包含在系统搜索路径中。

执行

	blogDayone2Hexo.py

好了，就这么简单，hexo格式的markdown源文件已经在

> source/\_posts

目录下面创建完毕了。文件名就是dayone里面一级标题的名称。二级标题以下级别都已经调整完毕，而且tags都搞定了。可以进去修改内容，或者直接

	hexo g
	hexo d

进行发布了，happy blogging! :-)

由于这里面涉及了几处技术问题的解决，因此我们展示一下解决的过程。作为一种技术经验的累积。

## 剪贴板的读写

有几种不同的方法，但是这一种显然最为有效，而且据说可以跨平台。我只在mac上面测试，其他平台请读者自行尝试。

	import subprocess
	
	def getClipboardData():
	    p = subprocess.Popen(['pbpaste'], stdout=subprocess.PIPE)
	    retcode = p.wait()
	    data = p.stdout.read()
	    return data
	
	def setClipboardData(data):
	    p = subprocess.Popen(['pbcopy'], stdin=subprocess.PIPE)
	    p.stdin.write(data)
	    p.stdin.close()
	    retcode = p.wait()

定义了上述函数之后，可以使用

	data = getClipboardData()

来获得剪贴板内容字符串。注意打印的时候应该采用

	for line in data.split('\n')

这样的方式，否则会出现乱码或者逐字打印等不符合预期要求的结果。

## 寻找特定目标

我们找的目标主要分为一级标题（对应文章题目）、二级以下标题（都需要提升等级）和tags。因此正则表达式显然是个好的选项。

	title1stlevel = re.compile("^\#\ ")
	titleMultiLevel = re.compile("^\#\#+\ ")
	tagInline = re.compile("^\#(?![\ |\#])")
注意一级标题是开头加#加空格，二级标题其他相同，但必须包含2个以上的#，而标签也是开头#，但后面既不能是空格，也不能是#。如果考虑不周全，可能会忽略一些特殊情况。

寻找的方法采用的是match函数

	for line in data.split('\n'):
	    if title1stlevel.match(line):
	        title = line[2:]
	    else:
	        if tagInline.match(line):
	            tags.append(line[1:])
	        else:
	            body.append(line)
注意这里一开始用了一个小技巧，所谓提升等级，实际上就是去掉最前面的一个#，就完全搞定了。 :-P

但是后来发现这样带来了反效果。我用的jacman主题里面，可以自动生成博文的目录结构。可是只有二级标题开始才可以正确识别。因此根本不必提升标题等级。于是干脆去掉了对于titleMultiLevel匹配成功的处理。 :-)

## 时间表示

因为我这里的目的是不再采用

	hexo new filename

这样的语句来生成文件，因此必须要自己插入时间。

插入的格式要完全按照hexo的要求，采用time.strftime函数可以轻松实现。

	import time
	datestr = "date: " + time.strftime("%Y-%m-%d %H:%M:%S") + "\n"

## 完整的源代码

我做了一个gitcafe项目，请参阅[这里](https://gitcafe.com/wshuyi/blogdayone2hexo/blob/master/blogDayone2Hexo.py)。

## 结语

附带说一句，本文就是用[blogDayone2Hexo.py](https://gitcafe.com/wshuyi/blogdayone2hexo/blob/master/blogDayone2Hexo.py)这个脚本转换成为了hexo源文件格式发布的。 :-)
