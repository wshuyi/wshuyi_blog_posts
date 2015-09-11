


title: title
title: Time Machine克隆Mac系统
date: 2015-08-07 20:01:20
categories:
- 技术点滴
tags: 
- mac
---




## 两台Macbook

![](http://7mnmvp.com1.z0.glb.clouddn.com/macbook_air_11inch_2012_04.jpg)

去年夏天，临出国的时候，我买了一台Macbook Air。实际上我的13寸Macbook Pro之前一直用得很舒服。虽然型号老了些，但是是2012年夏天升级了SSD之后，开启应用一般都是“唰”地一下。

买air的原因有2个：

1. 我的科研项目预算里面填写了设备经费，好几年了一直没动。因此打算买一台新的工作用电脑。
2. 让我在国外随身背着一个好几斤沉的Macbook Pro，实在有些残忍。我又不打算练习举重项目。 :-P

于是就买了11寸的Macbook Air。当时觉得有些古怪。面前突然放着两台电脑，都是苹果的。功能上面似乎也有很大的重叠。

但是，到了美国，真正启用这台Macbook Air的时候，感觉立刻就不一样了。太有科技感了！Macbook Air小小的身材非常轻盈，能干的事情却一点儿都不少。我用它记日记、查资料、看电影、整理照片、联系亲友、学课程、编程序、试软件、做研究、写报告……甚至还成功申请到了国家社科基金。 :-)

这一年，Macbook Air没有一次让我失望。总是能在我高负荷的使用强度之下保持良好的工作状态。

有的时候，早上一觉醒来，看到桌面上放着的这台小巧的笔记本电脑，真是有些疑惑。它真的这么强大吗？

只有看到最新版的Retina Macbook之后，我才觉得Macbook Air不再是最为轻盈的电脑了。但是今年新出的12寸Retina Macbook只有一个接口，限制着实太多了些，不符合我对工作用电脑的要求。

回国之后，惯性作用下我还是一直在使用Macbook Air。毕竟一台工作状态如此只好，携带又方便的电脑，为什么不用？

可是另一台Macbook Pro就比较尴尬了。被我扔在一边。回国之后只用过2次。

![](http://7mnmvp.com1.z0.glb.clouddn.com/macbook-pro.jpg)

第一次是看看还有没有电。事实证明，待机8个月还是做不到的。 :-P 

第二次是我需要拷贝一张DVD里面的内容出来，Macbook Air上面没有光驱……

![](http://7mnmvp.com1.z0.glb.clouddn.com/2000px_DVD_logo_svg.png)

Macbook Air一直作为我的唯一主力机工作。可是美中不足的是，它的屏幕确实太小了。11寸Macbook Air看电影上下没有余量。许多应用（例如网页浏览）必须全屏才能显示开。什么编辑器都得拼命加大字体，才能看着舒服。

所以，看着那台被我扔在柜子里许久的老Macbook Pro，我打算把它重新利用起来。
## 如何恢复工作环境

这一年，Macbook Air的OSX系统里面的内容发生了太多变化。

1. 操作系统系统升级到了10.10 Yosemite版本；
2. 卸载了许多不用的软件，同时安装了许多新的软件；
3. 我的工作流程重心发生了几次转移，最后落在了Ulysses上面，辅助的工具包括python, automator和alfred；
4. 虽然大部分的东西都云端化了，但是依然有许多工具、软件都是本地化的。

回忆一下，去年我刚买了Macbook Air的时候是怎么做的？是全新安装！为什么？就是因为之前对OSX系统不熟悉，安装软件的时候做了很多糊涂的事情，把系统的软件管理弄得乱七八糟。例如没有用brew管理软件，而是采用软件包解压编译的方式进行安装等。所以当时必须从头建构系统，可是花了不少心力，才最终让Macbook Air变得可用的。

让我再来一回？……算了吧。
## Time Machine，神奇时光机

![](http://7mnmvp.com1.z0.glb.clouddn.com/time_machine_logo.jpg)

Time Machine，苹果的时光机，杀手级应用。有人嫌它占地方大。在知乎上面问问题，说你们放着这么宝贵的移动硬盘空间，不去存储电影、音乐和资料，反倒给Mac用来做备份，不觉得浪费吗？

可想而知，他被Mac用户们骂了个狗血淋头。


![](http://7mnmvp.com1.z0.glb.clouddn.com/Grace-de-Leon-580x398.jpg)

一旦你的系统出问题了。例如机器被砸了、被抢了、被盗了、被水泡了……咱们就不描述这种让人悲痛欲绝的场景了。总之，这种悲催时刻，只要你还有一个Time Machine备份在手，那你无非也就是损失了一台几千元的（二手）电脑而已。因为你可以立即购买一台新的电脑，然后时间机器会把它变得跟你损失的那台机器（几乎）一模一样。这里加了个“几乎”，是因为需要考虑从你上次备份到发生惨剧之间，到底有多长时间？ :-P

你看，你的数据没有丝毫损失，同时又有了新电脑，要不要庆祝一下？

吹吧？不是吹。是真的。

我的电脑没有丢，但是我希望我的Macbook Pro能够和Macbook Air一样给我一个舒服的工作环境。我该怎么办呢？当然是使用Time Machine了。 :-)
## 要不要下载USB安装盘？

![](http://7mnmvp.com1.z0.glb.clouddn.com/Apple_USB_drive_640x360.jpg)

许多网上的经验帖子告诉我们，要使用Time Machine克隆系统，首先需要在新电脑（对我来说，是旧的Macbook Pro）上面抹盘安装一个全新的系统。之后执行迁移助手。

![](http://7mnmvp.com1.z0.glb.clouddn.com/osx_transfer_assistant.png)

我看了很疑惑，既然新电脑上面的系统本来也就是一个中转，会被Time Machine覆盖掉，那还费这个劲干啥？

于是，我查询到了另一个词“Recovery HD”。

## 恢复模式

原来Mac重启的时候，按住`⌘ + R`就可以进入这种恢复模式状态，可用于从Time Machine恢复数据。

我试了。Mac屏幕上首先出现了菊花。闪烁了一会儿，继续菊花……然后不闪烁了，一直菊花……

我愤怒了，于是继续查询。好在还有另外一种办法，就是开机的时候按住`⌥`，可以出现启动选项。教程里面说选项有好几个。我一看，这台Macbook Pro上就俩。一个是正常启动，一个是恢复10.9.2。哦，原来Macbook Pro上面的系统还是Mountain Lion的第二版啊。

点击进入，出现了恢复界面。我选择从移动硬盘上面的Time Machine恢复数据，目标自然是`Machintosh HD`。系统提示我会删除全部数据，我说没问题。

![](http://7mnmvp.com1.z0.glb.clouddn.com/2014032813514646.jpg)

然后就开始了漫长的等待过程。好在这个时候我的Macbook Air完全可用。我就干自己的事儿去了。

中午提示，还需要大约6个小时才能完成恢复。我一想，那就下午6点再见了呗。

没想到下午3点多突然响起了“duang”的一声，是系统启动音……

## Macbook Pro上面的Yosemite 10.10.4

我以为中途除了故障，正在懊恼。启动一看，跟我的Macbook Air上面系统一般无二。

![](http://7mnmvp.com1.z0.glb.clouddn.com/yosemite2_a4d810440ef3625c0b0f1b2c5973c3f8.jpg)

说明：上面这张图是我“借”来的。 :-P

底下的dock里面出现的都是新的应用，包含Ulysses，包含马克飞象，还包含……一个大问号！
## 遇到的一些问题

要说恢复得完美无缺，还是有些言过其实。就已知的一些问题，罗列一下解决方案吧。

### WIFI连不上了

![](http://7mnmvp.com1.z0.glb.clouddn.com/wifi631.jpg)


连不上也就罢了，居然提示“电缆被拔出”。连着电缆才能上网，那还叫WIFI吗？！

查了一下，原来是个已知问题。而且是升级到Yosemite之后的常见已知问题。

腾讯网有一篇教程：[教你如何自行修复Yosemite的WiFi问题](http://digi.tech.qq.com/a/20141029/010658.htm)，其中的解决方法1就完满地搞定了这个事儿。

精简后罗列一下：

1. 无线菜单项目中关闭WIFI。
2. 在Finder中执行`⌘⇧G`，并输入路径`/Library/Preferences/SystemConfiguration/`
3. 在开启的文件夹中选择下面这5个文件，备份后直接删除

	com.apple.airport.preferences.plist
	
	com.apple.network.identification.plist
	
	com.apple.wifi.message-tracer.plist
	
	NetworkInterfaces.plist
	
	preferences.plist

4. 重启Mac，开WIFI。

### iCloud要密码

![](http://7mnmvp.com1.z0.glb.clouddn.com/icloud_apple.png)

这个属于没办法的事情，为了安全起见嘛。虽然你拥有Time Machine，但不意味着你真的拥有对应的账户。不但iCloud，就连Facetime、iMessage都跑出来跟着凑热闹。一个个输入吧。

App Store下载并且购买的软件，例如Ulysses，在第一次启动的时候，也要求输入密码，确定用户的身份。

### Marked 2 大问号

为啥Marked 2的图标显示出来是个大问号呢？因为Marked 2的合法许可不见了。这软件是需要注册才能使用的，也不奇怪。

我尝试着从App Store恢复下载，才知道不是这么回事儿。我当时是先下载了一个试用版（正确），然后缴费成为正版用户（正确），可是缴费是在软件内部购买（错误）。这样App Store里面没有记录，所以必须手动下载。看来以后买Mac软件还是从App Store里面购买比较靠谱。

### Doit.im

![](http://7mnmvp.com1.z0.glb.clouddn.com/doitim.png)

突然发现许多早已挪动走，甚至是标记了已经完成的项目又都冒了出来。我很是纳闷儿。幸好其他同步都是正确的，因此也只是勾选了几个完成，没有造成太大的麻烦。

### Virtualbox找不到虚拟机文件

![](http://7mnmvp.com1.z0.glb.clouddn.com/ptxgwgvtycaizkaxapqx.jpg)


这个不赖OSX的恢复功能。因为是我把它们放在了Time Machine的范围外面。原因是每一次开启软件，总会有新的变动。于是Time Machine就要把这些变动都记录下来，比较麻烦。

既然如此，解决起来也简单，把对应的目录从Macbook Air拷贝到Macbook Pro就可以了。

## 不能忍的问题

这个问题可就不是前面那么简单了。任你脾气多好，恐怕也忍不了了。

那就是Time Machine出了问题。

我的计划是这样的，今后把厚重的Macbook Pro摆在我自己的桌面上面，出门带着Macbook Air。因此Macbook Pro的备份就跟Synology Data Station去做就好了。不需要平时连着一个移动硬盘，怪麻烦的。而带出门的Macbook Air要是打算备份的话，一个移动硬盘是不能少的。

可是，因为我用移动硬盘上面的Time Machine备份恢复了Macbook Pro，于是Macbook Pro把它作为了自己的Time Machine盘。打算承接之后继续备份。我没有答应。可是当我把它拿回去连接Macbook Air的时候，第一次启动备份居然用了半天。这让我有了很不好的预感。


![](http://7mnmvp.com1.z0.glb.clouddn.com/20150807_175706_snapshot_01.jpg)

果然，清理一些老旧备份，腾出空间之后，Time Machine的备份从0开始……

![](http://7mnmvp.com1.z0.glb.clouddn.com/20150807_183317_snapshot_01.jpg)

原来，Time Machine恢复的意义就是整体转移工作环境到新的电脑，包括备份盘。

Macbook Air的备份从下午3点多一直持续到了第二天上午10点，整夜无休。

至于Macbook Pro，那就更惨了。因为是无线方式，速度更慢。从几乎相同的开始时间，一直持续到第二天晚上7点多。当然，夜里没有开——因为风扇噪声太大了，吵得人睡不着觉。想想也确实为难我的老Macbook Pro了。大热天的，一边Time Machine备份，一边Dropbox重建文件索引。

幸好第二天是周六，白天没在家。等到晚上回来的时候，备份刚刚完工。 :-)

![](http://7mnmvp.com1.z0.glb.clouddn.com/13.01.09-Thunderbolt_Cable.jpg)

下次再换新机器，还是老老实实买（或者借？）一根Thunderbolt连接线好了。