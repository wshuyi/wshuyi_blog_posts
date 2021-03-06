

title: title
title: 把hexo blog从Dropbox中弄出去
date: 2014-11-14 16:28:22
categories:
- 技术点滴
tags:
- hexo
- dropbox

---


基于hexo的blog发布系统已经调整得非常完善了。目前可以在电脑和手机上轻松进行访问，界面都已经根据设备进行自动适配。而且如果hexo blog放在Dropbox中，那么就可以自动在dropbox里面进行备份。这样数据就会获得最大的安全。

然而今天我把hexo blog从dropbox里面弄出去了。原因是什么呢？主要是因为每次hexo g与hexo d生成了太多的目录和文件。因此每次需要弄几千个文件在dropbox里面同步。这样带来很大的问题，就是需要耗时许久才能完成。这样许多亟需更新备份保留的文件反而不能及时同步，带来很大的信息安全隐患。另外新加入的图片也不能立刻上传到repo中，这就带来另外一个问题，就是这边刚刚改动hexo blog发布之后，再写新的blog或者其他内容，都不能马上获得正确的预览。这当然不好，因此我这两天实际上一直都在思考如何解决这个问题。

一开始，我打算用最低的成本来完成这个事儿，就是把public, .deploy等文件夹搬出去，然后进行符号链接。这样总体目录都不用动了。但是后来发现这还是会带来问题。内部的github备份机制还会产生其他的文件，每次dropbox同步依然耗时不菲。而且我现在已经有4个不同的blog文件了，每一个要是都弄几个不同层次的内部文件夹扔在外面，不论是管理还是维护都是个负担。

后来我决定倒过来想想，就是首先把hexo blog整个儿扔到Documents文件夹下面。这样最大的好处就在于以后发布的工作本质上跟dropbox无关了，而且完整保护目录结构。

然后采用关键备份。什么是关键？首先当然是我的blog内容了。这里都是采用markdown格式，放在 source/\_posts 下面。于是我重新在原先blog的地方建立hexoBlog目录，并且根据博客账户分别建立目录，然后把\_posts文件夹拷贝过来，并且在Documents/blog/xxx/source/目录下面建立\_posts符号链接。这样，我依然是修改源文件，但是源文件保存在了dropbox里面。生成的那些繁复的路径和文件就不再由dropbox处理了。

但是事情做到这里还不算完，因为必须考虑还有个配置文件。配置文件分在两个级别。首先整个博客的配置，它包含了github与gitcafe账号设置、主题选择、个性化内容等。另外我选择的jacman主题本身也有一个配置文件，这个文件主要包括对jacman主题下面一些社交网络与分享工具（例如多说等）的账号设置等。另外别忘了我把author logo调整为了我自己的头像，因此这个img/author.jpg也得保留。

如此一来，以后如果发生数据灾难，只需要在Documents下面重建blog目录，hexo init后建立符号链接，拷贝配置文件（或者从中拷贝配置内容），然后就可以自由进行部署了。

困扰我多日的问题至此解决了。 :-)
