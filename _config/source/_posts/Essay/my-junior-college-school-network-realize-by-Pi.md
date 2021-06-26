---
title: Raspberry 安装pptp服务
date: 2019-03-14 12:18:27
tags: Junior College Network
---

# 异曲同工实现代理连接
今天实现了8个月之前没有实现（完成）的事情，并且在舍友的帮助测试下，与期望相同，心中忍不住窃喜。

总共耗时不到一天，参考了很多文章，最后才知道重点是PPTP,也走了很多弯路(安装了一个pptp-linux,我不知道是什么)，因为完全是自己摸路，碰壁是肯定的，如果一个人告诉你，你直接去安装PPTP服务，配置3个文件,那就是几分钟的事情。

首先值得可喜的是，我发现了vim/vi之外的一个编辑器，那就是nano。用了几次，查了一些用法，在配置过程中，觉得比vim更容易上手(使用nano下面有操作快捷键说明)。今天还去上了Linux课，老师简单的讲了一下vim，在编辑器中，演示了简单的增删查改操作。

------

*我在配置过程中最具有价值的参考连接:*

**[UBNT](https://help.ubnt.com.cn/hc/zh-cn/articles/206123162-EdgeMAX-PPTP-Server-VPN-%E9%85%8D%E7%BD%AE%E6%A1%88%E4%BE%8B)(网络拓扑图的结构)**

**[Über mich](https://jankarres.de/2013/12/raspberry-pi-pptp-vpn-server-installieren/)(借鉴sudo nano /etc/pptpd.conf ip的更改)**

**[Domoticz](https://www.domoticz.com/wiki/Installing_a_PPTP-VPN_server_on_a_Raspberry_Pi)(最后一步起关键作用，后面会讲)**

配置的内容，这里简要概括一下作用，后面详细步骤解说
> *  /etc/pptpd.conf  #配置路由器分配给你的ip地址
> *  /etc/ppp/pptpd-options #配置ms-dns
> *  /etc/ppp/chap-secrets #配置用户名和密码

## 安装pptpd
```
apt-get install pptpd
//有提示要输入y,都是输入y 就可以了
```
### 配置过程

#### 1. 配置/etc/pptpd.conf
```
sudo nano /etc/pptpd.conf
//使用方向键移到配置文件的末尾,增加两个信息
localip 192.168.199.203 //这个根据路由器分配给Pi的IP地址填写
remoteip 192.168.199.234-238,192.168.199.245
```

#### 2. 配置/etc/ppp/pptpd-options
```
sudo nano /etc/ppp/pptpd-options
//使用方向键移到配置文件的#ms-dns处，增加两条信息（也可以去掉配置文件中#修改）
ms-dns 8.8.8.8
ms-dns 8.8.4.4
//dns地址的配置也可以用其它的
```

#### 3. 配置/etc/ppp/chap-secrets
```
sudo nano /etc/ppp/chap-secrets
添加用户名和密码的配置
如:
null pptp 123456789 *
```

## 查看PPTP服务的运行状态
```
systemctl status pptpd.service
//这个命令很重要,运行后可以通过这条命令显示的状态，还可以查看报错的一些相关内容(ms-dns 写成ms-dsn 、无法识别配置ms-dsn等)
```

## 修改sysctl.conf
```
sudo nano /etc/sysctl.conf //找到net.ipv4.ip_forward=1 去掉#（注释）
sudo sysctl -p //应用配置
```

## 更改防火墙规则
```
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## 重启PPTP服务
```
sudo /etc/init.d/pptpd restart  
```

**最后到路由器设置端口转发(根据舍友的测试反应，如果关掉端口转发则无法连接)**

同时感谢师弟，借树莓派一用，不然也不可能完成以上这些东西呢。
