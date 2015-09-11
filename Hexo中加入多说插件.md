


title: title
title: Hexo中加入多说插件
date: 2015-08-11 18:26:16
categories:
- 技术点滴
tags: 
- Hexo
- 多说

---

更新到了最新版的Hexo之后，其他还好，就是我的多说插件找不到了，比较郁闷。因为这样一来，我就没法跟读者互动了。

解决的办法，自然还是从配置文件上面找。奇怪的是新版Hexo的配置文件`_config.yml`里面别说是多说了，就连默认的disqus插件都不见了。

哪儿去了？

看了一下多说官网上面的[介绍](http://dev.duoshuo.com/threads/541d3b2b40b5abcd2e4df0e9)才知道，原来直接把

	duoshuo_shortname: 你站点的short_name

填写到配置中就可以了。

![](http://7mnmvp.com1.z0.glb.clouddn.com/2015-8-11_18-21-44_snapshots-01.jpg)

照做以后，重新部署。再来看看之前的blog：

![](http://7mnmvp.com1.z0.glb.clouddn.com/2015-8-11_18-25-55_snapshots-01.jpg)

成功！