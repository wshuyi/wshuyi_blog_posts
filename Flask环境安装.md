

title: title
title: Flask环境安装
date: 2015-01-26 21:52:47
categories:
- 技术点滴
tags:
- flask
- python


---

本教程包含本地macbook与远程digitalocean的flask环境安装设置。

## 缘起

我喜欢读阳志平的博客。去年寒假的时候每天晚上抱着iPad读里面的文章，不亦乐乎。后来阳志平弄了个微信订阅号产品，叫做“安人心智”，其中[有一期](http://mp.weixin.qq.com/s?__biz=MzA3Mjk0MTcyNg==&mid=201765895&idx=1&sn=a95a6273891df4b7429312df482857c5#rd)提到了大量的[python书籍](http://importpython.com/books/?nsukey=DOMCGSwXwI7w2R5%2Fa%2FxHJ4AR6XjtWDDU%2FopFqzx1k8ezeWW03hg8SXDrGLDJ4y43ZMHcywv8TQdjsJSdmIyveQ%3D%3D)，最后吐槽说学这本书也是迫在眉睫了，便是指的Flask。

![](http://7mnmvp.com1.z0.glb.clouddn.com/flaskbookCover.jpg)

当时看这个火箭一样的封面觉得很有趣。后来学了一些ruby框架，尤其是Sinatra，常有人拿Flask来对比。我觉得Python我用的更熟一些，何不学习一下呢？这样我将来讲信息系统开发的时候，便有一个很好的系列教程可用了。现在课程上机部分虽然内容比较新颖，但是东一榔头西一棒子总还是需要系统化一些。

## 机会

code school下午给我发来一封信，愉快地告诉用户们它被Pluralsight并购了。作为庆祝可以72小时使用新东家的课程产品，不用花钱。于是我上Pluralsight去看看都有啥新的课程，结果发现上面讲解Flask。这个不错，因为我之前在mooc上面搜索，没有找到对应课程，不妨学习一下。

## 尝试

既然有这么好的教程，我于是就按照教程里面一步步安装。python是现成的，只需要安装virtualenv, virtualenvwrapper，以及flask不就好了吗？可是事实上远没有那么简单。

### anaconda 与 virtualenv 的问题

按照教程，


	pip install virtualenv

提示virtualenv在anaconda里面是beta版本不稳定，要不要试试anaconda自己的虚拟环境？当时我选择了否。因为我既不打算把很好的mac上anaconda环境破坏掉，同时也不打算学习一个新的虚拟环境配置。

### boot2docker 占用内存过大

于是那就用docker吧。反正boot2docker已经安装了好几天了，好像还没有正式启用呢。

建立了一个目录，叫做figtest，里面根据教程[Fig | Fast, isolated development environments using Docker](http://www.fig.sh/index.html) 中quick start章节的内容建立了4个文件：

`Dockerfile`


	FROM python:2.7
	ADD . /code
	WORKDIR /code
	RUN pip install -r requirements.txt


requirements.txt


	flask
	redis

app.py


	from flask import Flask
	from redis import Redis
	import os
	app = Flask(__name__)
	redis = Redis(host='redis', port=6379)
	
	@app.route('/')
	def hello():
	redis.incr('hits')
	return 'Hello World, Shuyi! I have been seen %s times.' % redis.get('hits')
	
	if __name__ == "__main__":
	app.run(host="0.0.0.0", debug=True)


fig.yml


	web:
	  build: .
	  command: python app.py
	  ports:
	"5000:5000"
	  volumes:
	.:/code
	  links:
	redis
	redis:
	  image: redis


建立之后就执行


	fig up


下载东西挺慢的，等了半天，去吃饭了。

我吃饭回来，安装过程终于搞定了。也运行起来了。可是不知为啥，我发现电脑特别慢，卡死一般。自从我用macbook，还很少遇到这种情况。后来打开了virtualbox查看，倒吸一口凉气啊。boot2docker虚拟机默认占用内存2个G，据说随着开启container数量增多，自己还能往上追加。mac自身应用一大堆，这就导致内存捉襟见肘了。看来在macbook air上面使用boot2docker似乎有些不大靠谱。如果是16G内存的macbook pro，那自然就是另外一番景象喽。 :-P

## 第一步解决方法

这是到今晚为止我做出的解决办法，未必完美，但是我觉得挺好用的了。 :-)

### conda 自己的 virtual 环境

首先是本机上，我需要一个开发环境。既然docker在我的macbook air上不是办法，我又不打算抛弃anaconda，那就用anaconda提供的virtual环境好了。这篇教程[Using the Anaconda Python Distribution - Dave Behnke](http://davebehnke.com/using-python-anaconda-distribution.html)写的非常详细，因此不存在麻烦的问题。有了这样一个隔离环境，安装啥东西就都好办了。


	conda create -n flask python
	source activate flask


新建一个环境，名字叫做flask，它首先包含python，这里可以指定python版本，默认就是跟anaconda系统安装的一致，是2.x系列。


	(flask)➜  flask  conda info -e
	conda environments:
	
	flask                 \*  //anaconda/envs/flask
	root                     //anaconda


如果打算停用当前环境，可以


	source deactivate

如果打算彻底删除当前环境，可以

	conda remove -n flask --all


当然我们现在没有停用或者删除的必要，在环境里面可以安装flask了


	conda install -n flask flask

前一个flask是环境名称，后一个才是包的名称。

这就行了，我们可以随便创建一个目录，例如叫做 `~/learn/flask`

里面创建一个 helloworld.py


	from flask import Flask
	
	app = Flask(__name__)
	
	@app.route('/index')
	def index():
	return 'Hello, Shuyi!'
	
	if __name__ == '__main__':
	app.run()


保存好以后执行


	(flask)➜  flask  python helloworld.py 
 - Running on http://127.0.0.1:5000/


在浏览器里面键入相应地址

![](http://7mnmvp.com1.z0.glb.clouddn.com/flaskTestIndexLocalhost.jpg)


### digitalocean上面的docker

#### 系统升级

好长时间没有接入 digitalocean 上面的ubuntu镜像了，因为准备安装 docker， 所以习惯性进行升级。


	apt-get update
	apt-get upgrade

结果更新重启后提示我说我现在用的12.04版本ubuntu已经不再提供支持了，要不要更新到14.04呢？我觉得可以，就更新了。经过了漫长的更新过程后，测试一下，原先的vpn还能正常使用，于是就进行了snapshot，将来如果出问题，还能回到现在这个状态，挺好的。 :-P

#### docker 和 fig 安装

我原以为


	apt-get install docker


就可以了，结果一执行就告诉我docker没安装，可以通过


	apt-get install docker


来安装，可我就是那么做的啊。半天挠头之后，上网看一眼教程，立刻傻眼了，安装的命令居然是


	apt-get install docker.io


这才会真正安装docker及其一大堆依赖包。好吧。


	pip install fig


好了，需要安装的基本就是这些。

#### 文件传递

我这里本地已经有一个figtest目录了，就不打算重新录入到远端了。可以使用scp命令完成这一过程


	scp -r figtest root@162.XXX.XXX.XXX:/root/


#### 执行 fig


	ssh root@162.XXX.XXX.XXX
	cd figtest
	fig up


好了，又是一通从网上下东西，然后一层层设置。不过实话实说，比我这儿本地docker下载文件快多了，不愧是机房的网络啊，快！

很快就弄好了，已经启动了服务器。

浏览器里面打开看看。

![](http://7mnmvp.com1.z0.glb.clouddn.com/flaskTestIndexDigitalOcean.jpg)

一切正常，好了。

C-c 暂停服务，键入


	fig stop


注意可以通过修改 figtest 下面的文件后重启fig up，来试验新的代码。这其实都是因为在 fig.yml里面设置了volume的作用。这样docker虚拟机最顶层用的就是本地目录下面全部文件最新的代码。