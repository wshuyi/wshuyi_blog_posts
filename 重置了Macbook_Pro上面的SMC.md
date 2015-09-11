

title: title
title: 重置了Macbook Pro上面的SMC
date: 2015-08-09 18:15:03
categories:
- 技术点滴
tags: 
- mac
- smc
- 休眠


---



在macbook pro上面恢复了osx 10.10.4之后，出现了至少2次休眠后无法唤醒的问题。最后决定不忍了。

查了一下，发现是SMC有问题。于是重置一下。

重置的方法参考[重置 Mac 上的系统管理控制器 (SMC) - Apple 支持](https://support.apple.com/zh-cn/HT201295)，简单说就是：

1. 关机
2. 接通电源
3. 按`⇧^⌥`和电源键，然后都松开
4. 按电源键开机

重启一下，到目前工作还算良好。又找到了一篇[关于基于 Intel 的 Mac 电脑的 EFI 和 SMC 固件更新 - Apple 支持](https://support.apple.com/zh-cn/HT201518)，对比一下，发现目前我机器上面的SMC固件比这篇文章里面提供的还要高一些。 :-)

![](http://7mnmvp.com1.z0.glb.clouddn.com/20150809_182403_snapshot_02.jpg)