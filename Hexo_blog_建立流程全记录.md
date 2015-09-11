

title: title
title: Hexo blog 建立流程全记录
date: 2014-01-01 20:59:38
categories:
- 技术点滴
tags:
- hexo
- blog
- github
- gmail

---

这个教程主要是讲如何在一个机器上面利用多个github 账号建立多个不同的 hexo blog，让它们之间相互不影响。可以让平时需要记录的信息产生分流。

## 安装hexo

从略，因为hexo自身的教程写得太清楚了，重复起来没有意思。

## 申请一个Gmail

当然，可以申请任何邮箱。但是gmail的好处不必多说。而且不像原先控制那么严格，Gmail几乎可以随便申请了。中间需要填写一个手机号码，我4个邮箱用的1个手机号码。只有最后一次要求我短信验证。

为了后面叙述方便，假设邮箱账号设置为 myaccount1 吧。

## 申请一个 github

如果运气好的话，github上面的账号名称可以和gmail相同，那样就好办多了。

申请成功之后，创建一个repo，repo的名字一定要取 myaccount1.github.com，然后记得要把页面上面对应的ssh地址拷贝下来备用。

	https://github.com/myaccount1/myaccount1.github.com.git

## 建立ssh key

	cd ~/.ssh
	ssh-keygen -t rsa -C 'myaccount1@gmail.com'

注意生成的文件名称不要用默认的 `~/.ssh/id_rsa`，改成 `id_rsa_myaccount1`，之后 .ssh目录下面就会出现两个新的文件，一个叫做 `id_rsa_myaccount1`， 另一个叫做 `id_rsa_myaccount1.pub`

执行

	ssh-add id_rsa_myaccount1

然后打开 `id_rsa_myaccount1.pub`

把其中的全部内容复制，上 github，在 account setting 里面添加 ssh key

名字一栏随便填写，就是个记号， 例如可以叫做 myaccount1 on win 等。

然后内容里面把剪贴板里面的东西粘贴进来。保存。

在 ~/.ssh 目录下面新建/修改 config 文件

追加以下内容

	# comment blablabla (myaccount1@gmail.com)
	Host github-myaccount1
	HostName github.com 
	User git 
	IdentityFile ~/.ssh/id_rsa_myaccount1

保存

## hexo blog 建立

创建一个目录，我喜欢在 blog 目录下面新建 myaccount1目录。这样既便于集中管理，同时又可以清晰对比，分门别类。

进入 blog/myaccount1，执行

	hexo init

然后修改 `_config.yml` 的最后 deploy 部分，

改为

	deploy:
	  type: github
	  repository: git@github-myaccount1:myaccount1/myaccount1.github.com.git
	  branch: master

尤其注意第三行中的

	github-myaccount1

原先从github当中保留下来的ssh地址应该是

	git@github.com:myaccount1/myaccount1.github.com.git

但是由于在本机上面有多个github账号，因此必须予以区别，原先github.com的写法就不能要了，代之以在 ~/.ssh/config 中进行的重命名。

## 测试

修改 `_config.yml` 中的博客名称和作者等必要信息

执行

	hexo g
	hexo d

成功。

注意第一次生成博客需要等10分钟，心急吃不了热豆腐。 :-P

## 后续工作

这样做有个问题，就是占用了许多免费资源。我也怕 Google 会因为长期不活跃登录，收走我的邮箱账号。虽然我觉得大公司不至于如此小气。以防万一吧。

到 gmail 中，设置 -\> 转发。 把所有的邮件转发到自己的主邮件去。 这样一来时常会有操作。而来即便Google要收账号，肯定也得通知。可以第一时间获知，采取对策。

还有，别忘了验证 github 邮件。这个确实很容易遗忘，呵呵。github会提醒你的。