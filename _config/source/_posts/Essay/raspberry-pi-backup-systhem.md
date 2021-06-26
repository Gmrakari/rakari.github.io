---
title: raspberry_pi_backup_systhem
date: 2019-04-27 00:34:36
tags:
---
RaspberryPi备份系统的方法
1、Win32DiskImager来备份树莓派镜像文件
2、DiskGenius
3、ubuntu下用dd命令

以上这几种，我个人认为第三种最适合我了。
首先提一下优缺点，第一种Win32DiskImager，这个是把整个内存卡的内容cp下来（致命弱点），因为如果你的内存卡32G，那拷贝速度，还有还原的时候，需要一张一模一样或者更多内存的内存卡，优点就是操作简单，在window下备份速度应该较快。

第二种，没有试过，但是感觉，也不太理想。

第三种，感觉最折腾，但方便以后备份还有让自己从Centos中，第一次在虚拟机上用Ubuntu桌面版，之前好像在服务器上使用过,但体验感极差

配置了sudo


df -h查看详细分区（树莓派的系统区）
$ sudo dd if=/dev/sdc | gzip>/home/rakari/raspberry.gz


**参考**[制作树苺派SD卡备份镜像——树苺派系统备份与还原指南][来自：http://blog.lxx1.com/1450]

#更新
树莓派自带copy sd卡的操作 十分方便
直接用读卡器插上tf卡 用树莓派里面一个sd card copy的软件 （VNC或者直接用连接显示器可以打开看到该软件）
之前折腾那么多，还不如这个软件强大...
