---
title: 向量处理机
date: 2018-08-23 19:42:54
tags: Computer Architeture
---

# **向量处理机**  #

## 互连网络
SIMD系统的互连网络的设计目标是：结构不要过分复杂，以降低成本；互连要灵活，以满足算法和应用的需求；处理单元间信息交换所需的传送步数要尽可能少，以提高速度性能；能用规整单一的基本构件组合而成，或者经多次通过或者经多级连接来实现复杂的互连，使模块性好，以便于用VLSI实现并满足系统的可扩充性。
###  基本的单级互连网络 ###
 1、 立方体单级网络 2、PM2I单级网络 3、混洗交换单级网络 4、蝶形单级网络 主要是前面3种（ps:修改了图片的样式，然后今天数据库的课，我选择不去了，搞完这些东西先) 
![SIMD向量处理机——计算机互连网络.jpg](http://pe3qooug9.bkt.clouddn.com/SIMD%E5%90%91%E9%87%8F%E5%A4%84%E7%90%86%E6%9C%BA%E2%80%94%E2%80%94%E8%AE%A1%E7%AE%97%E6%9C%BA%E4%BA%92%E8%BF%9E%E7%BD%91%E7%BB%9C.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)
#### 1、基本的单级互连网络 ####
![1-1立方体互连网络.jpg](http://pe3qooug9.bkt.clouddn.com/1-1%E7%AB%8B%E6%96%B9%E4%BD%93%E4%BA%92%E8%BF%9E%E7%BD%91%E7%BB%9C.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)
这个是最简单的一种，只要画出一个三维立方体结构就可以写出互连函数了

##### 下面是Cube（0） 和 Cube（1）的互连方式 #####
![1-1立方体互连网络2.jpg](http://pe3qooug9.bkt.clouddn.com/1-1%E7%AB%8B%E6%96%B9%E4%BD%93%E4%BA%92%E8%BF%9E%E7%BD%91%E7%BB%9C2.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)

![1-1立方体互连网络3.jpg](http://pe3qooug9.bkt.clouddn.com/1-1%E7%AB%8B%E6%96%B9%E4%BD%93%E4%BA%92%E8%BF%9E%E7%BD%91%E7%BB%9C3.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)

##### 2、PM2I单级网络 #####
![1-2PM2I单级网络1.jpg](http://pe3qooug9.bkt.clouddn.com/1-2PM2I%E5%8D%95%E7%BA%A7%E7%BD%91%E7%BB%9C1.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)
这个主要是把函数的表达式写出来，通过计算，就知道他们的互连情况了

##### PM2I互连网络的部分连接图 #####
![1-2PM2I单级网络2.jpg](http://pe3qooug9.bkt.clouddn.com/1-2PM2I%E5%8D%95%E7%BA%A7%E7%BD%91%E7%BB%9C2.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)

##### 3、混洗交换单级网络 #####
![1-3混洗交换单级网络1.jpg](http://pe3qooug9.bkt.clouddn.com/1-3%E6%B7%B7%E6%B4%97%E4%BA%A4%E6%8D%A2%E5%8D%95%E7%BA%A7%E7%BD%91%E7%BB%9C1.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)
![1-3混洗交换单级网络2.jpg](http://pe3qooug9.bkt.clouddn.com/1-3%E6%B7%B7%E6%B4%97%E4%BA%A4%E6%8D%A2%E5%8D%95%E7%BA%A7%E7%BD%91%E7%BB%9C2.jpg?imageMogr2/auto-orient/thumbnail/!60p/rotate/360/background/I0ZGRkZGRg==/blur/1x0/quality/75|imageslim)
有单级互连网络，后面也有多级互连网络，但是多级的实在是太复杂，以后有空，我再把多级互连网络给总结出来

[参考：重庆大学网络教育](http://kjwy.5any.com/jsjxtjg/content/06/060105.htm)
