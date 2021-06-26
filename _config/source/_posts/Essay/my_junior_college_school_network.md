---
title: 攻破宿舍内网
date: 2018-09-14 08:57:36
tags: Junior College Network
---

## 我寻到什么? ##
其实我用了两个星期左右，了解到一点皮毛的东西，现在准备看完本校图书馆现存的4本左右的防火墙和虚拟网络的书籍（校图书馆的计算机书籍很全，👍）来加强基础知识和彻底了解虚拟网络的实现原理
每个人都有影响很深刻的书籍，我最近看林纳斯的自传（Just For Fun,以后英语水平达到一定程度，一定拜读原版和他和安德鲁的辩论之争），那个家伙真是令我感叹和敬佩，好令人向往的生活，目前来讲，这本是我重新对计算机另有看法的一本书了。
 <font size=2>（ps:蹩脚的文字，还有些乏味)</font><br>

**我通过阅读以下的文章得出的结论，可能有些草率或者总结的不足，欢迎e-mail给我补充或者更改错误**
![principle_dns_channel.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/principle_dns_channel.png)
![review_web_dns_principle_.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/review_web_dns_principle_.png)
以我的理解，能在宿舍上网，其实是分三大种
第一种，在局域网内架设出一个虚拟网络
第二种，利用校园网内网映射出对外开放的端口
第三种，dns隧道

### 1、在局域网内架设出一个虚拟网络 ###

引语：这个是我目前正在使用的一种方法，前提你必须能有一个利用局域网的地方，就是有水晶口插网线的地方，并且学校开放该插口的网络服务，例如：实训室开放的实验室，社团基地，学生干部办公室等地方。这个想法也来源于我哥，他跟我讲，如果你有一个地方可以上网，你就可以在那搭建一个服务器出来，我就想到了我的社团基地。后来，我马上电联YiGa学长(社长),我跟他讲，我需要用社团的网络架设一些东西，问他是否允许，他说可以，然后我就回宿舍拿笔记本过去社团基地，准备架设工作。当我进去，发现路由器厂家的名字很熟悉，之前在破解路由器网无意看到过，然后这一切，好像我看过的一本小说，事情的内幕慢慢涌现在我的眼前，使得我心理杂乱无比，加之快要成功的窃喜，肾上腺素不停在分泌，脸不停在烧灼，烫的不行。因为前人（社长），已经搭建好这一切，我只要设置一个账户密码，我就可以在宿舍，或者学校任一个使用这个账户密码上网了。

#### 正文 ####
通过一个刷好固件的路由器，通过路由器架设一个虚拟网络，使用路由的本地WAN地址，在局域网内，通过路由的本地ip，进行上网，这个方法实质就是：只要你在校园内，你通过VPN，就相当于从你连接的那一端拉一根网线连接到社团的路由器，然后使用路由器的网络服务上网。这个方法由于实现比较简单，我就附图片就好了

Step1:社长买的路由器网关是：192.168.199.1，输入密码登入后台
![路由的网关.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E8%B7%AF%E7%94%B1%E7%9A%84%E7%BD%91%E5%85%B3.png)

Step2:点击只能插件，进入路由器已经刷好的固件或者可以安装的插件
![智能插件.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E6%99%BA%E8%83%BD%E6%8F%92%E4%BB%B6.png)

Step3:这个插件社长已经安装好了，怎么安装过程我也不过多赘述了
![服务器插件.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%8F%92%E4%BB%B6.png)

Step4:添加账号和密码，保存就可以了
这个账号和密码就是登陆使用的（后面再解释）,差不多已经完成了，是不是很简单。。。
![配置账号和密码.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E9%85%8D%E7%BD%AE%E8%B4%A6%E5%8F%B7%E5%92%8C%E5%AF%86%E7%A0%81.png)

Step5:添加在"网络和Internet设置"添加一个vpn连接就可以了
![打开网络和Internet设置.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E6%89%93%E5%BC%80%E7%BD%91%E7%BB%9C%E5%92%8CInternet%E8%AE%BE%E7%BD%AE.png)

Step6:最后一步，根据添加的账户的密码，#按照指定位置填写就可以了，这样，在校园内都可以通过这个账号上网了，只要社团的路由器不断电，就可以实现24h不限制上网
![服务器配置示意图.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%85%8D%E7%BD%AE%E7%A4%BA%E6%84%8F%E5%9B%BE.png)


### 2、利用校园网内网映射出对外开放的端口 ###

引语：这个方法我测试了好多遍诶，并且在n次的实验结果下，我得出一个结论：我学校的内网映射出对外开放的端口中，没有开放udp 53、67、68，但是我在校园网内使用网络命令查看，第一次却有68（后面怎么测试，都没有68），莫名奇妙的期待中，测试了很多次，发现都不行，很绝望,不过没有关系，可能你们的学校可以呢,这个方法对于没有社团基地的朋友可以尝试一下，最后感谢日本大学的这个开源项目，使得我们能够使用这些，以后我也要使用这种开源协议，给初学者带来太大帮助了

#### 正文 ####

##### 1、PC端扫描 #####
连接校园网的情况下，先不用登陆账号验证
在pc端打开cmd，通过cmd使用网络命令
```
netstat -an  //查看udp开放的端口
```
结果如下图所示，只要关注udp开放的端口就可以了，如果看到53，67，68的关键字眼，那么恭喜你；如果没有，其实还可以通过测试配置文件，测试一把。
![netstat_an查看udp端口.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/netstat_an%E6%9F%A5%E7%9C%8Budp%E7%AB%AF%E5%8F%A3.png?x-oss-process=style/Hexo&Expires=1545360956&OSSAccessKeyId=TMP.AQGCh4btlfiAp1BAYIBJ_Yd4wgyWLJs8EpW8gAalr4FGjhzOwubi8IJGi-BrADAtAhQzub_WodaET7cgSbEPkYTBJChS3AIVAIesKAlCNjC3ERs-SDUR8um9jTSm&Signature=LhVuN%2Bn%2FkVCS4M9w0MOrPtRfWBU%3D
)

##### 2、Android端扫描 #####
手机版测试udp开放端口，APP：IP Tools
连接上校园网WiFi，可以看到自动分配的一个ip地址——中间ip内部地址那栏，把它复制下来，一会扫描端口的时候使用到,比如下面这个图的ip地址是：192.168.137.238
![ip_tools_uesr_image.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/ip_tools_uesr_image.png?x-oss-process=style/Hexo&Expires=1545361058&OSSAccessKeyId=TMP.AQGCh4btlfiAp1BAYIBJ_Yd4wgyWLJs8EpW8gAalr4FGjhzOwubi8IJGi-BrADAtAhQzub_WodaET7cgSbEPkYTBJChS3AIVAIesKAlCNjC3ERs-SDUR8um9jTSm&Signature=UQqkBxT7tThZwBaff4kHrxfsfLE%3D
)

进入旁边的扫描端口
![端口扫描.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/%E7%AB%AF%E5%8F%A3%E6%89%AB%E6%8F%8F.png?x-oss-process=style/Hexo&Expires=1545361079&OSSAccessKeyId=TMP.AQGCh4btlfiAp1BAYIBJ_Yd4wgyWLJs8EpW8gAalr4FGjhzOwubi8IJGi-BrADAtAhQzub_WodaET7cgSbEPkYTBJChS3AIVAIesKAlCNjC3ERs-SDUR8um9jTSm&Signature=jIXYoloeW0Ckj%2BUmmREzAt2yQ2A%3D
)

使用刚刚复制的ip内部地址，填写进去，然后按扫描
![ip_tools_uesr_image_填写主机ip地址.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/ip_tools_uesr_image.png?x-oss-process=style/Hexo&Expires=1545361103&OSSAccessKeyId=TMP.AQGCh4btlfiAp1BAYIBJ_Yd4wgyWLJs8EpW8gAalr4FGjhzOwubi8IJGi-BrADAtAhQzub_WodaET7cgSbEPkYTBJChS3AIVAIesKAlCNjC3ERs-SDUR8um9jTSm&Signature=4ShtL6yqRwpPlKi3AmKPqZ4WuwY%3D
)

这个是扫描后显示的端口，如果看到53,67,68，说明抱有一些希望，如果没有也不用紧
![ip_tools_uesr_image_scan_result.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/ip_tools_uesr_image_scan_result.png?x-oss-process=style/Hexo&Expires=1545361118&OSSAccessKeyId=TMP.AQGCh4btlfiAp1BAYIBJ_Yd4wgyWLJs8EpW8gAalr4FGjhzOwubi8IJGi-BrADAtAhQzub_WodaET7cgSbEPkYTBJChS3AIVAIesKAlCNjC3ERs-SDUR8um9jTSm&Signature=uwjp6%2BhhzYXcCldV0pJmBMNQeak%3D
)

**以上两种扫描其实都可以跳过，为了熟练几种网络命令罢了**

下面说怎么使用Openvpn吧，官方文档需要翻墙才能查阅
Centos安装Openvpn的教程直接贴我看过，觉得比较好的文章吧，省心又省力
直接介绍window的Openvpn的安装过程
点击旁边的下载就可以了  **[Openven安装包](https://pan.baidu.com/s/1S8XtfOLjepUlj3N1QYgmIA)**
解压安装包，默认选择里面的，点击next就好了
![default_choose_.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/default_choose_.png?x-oss-process=style/Hexo
)
安装目录选择默认或者自定义，不会的话，就直接默认，然后install
![path_choose_random.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%94%BB%E7%A0%B4%E5%AE%BF%E8%88%8D%E5%86%85%E7%BD%91/path_choose_random.png?x-oss-process=style/Hexo)
安装完之后，打开Openvpn，然后找到文件的所在目录，把配置文件放在config文件夹下面，然后就可以在小电脑图标右键打开connect，进行测试，看小电脑是否变成绿色，如果变成绿色，那么就说明成功，这样实现，24h无限制上网了，但是速度受限于服务器的宽带速度，如果像是1兆的毛细血管宽带，还是影响体验上网的乐趣的。





服务器那边安装openvpn,可以借鉴以下作者的文章，我也不在赘述<br>
[土豆不好吃](https://www.bennythink.com/softether-vpnserver.html)
[玖洲维城网络科技:绕过udp校园网](https://blog.csdn.net/qq_35422558/article/details/78018089)
