---
title: raspberry_pi_apt-get_update
date: 2019-04-27 00:30:14
tags:
---
查看系统信息
```
sudo lsb_release -a
```
**显示**
```
Distributor ID: Raspbian
Description:    Raspbian GNU/Linux 9.4 (stretch)
Release:        9.4
Codename:       stretch
root@raspberrypi:~#

```
**备份**
```
cp /etc/apt/sources.list /etc/apt/sources.list.bak <!-- cp备份一下源文件 -->
```

**最后**
```
root@raspberrypi:~# apt-get update
```
