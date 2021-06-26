---
title: Hanoi(汉诺塔)问题
date: 2018-12-21 13:18:04
tags: 递归与分治的调用
---
本人又参加了蓝桥杯了。这次是为第X届准备
为了这届不留遗憾，还是想努力一些，多做点题，争取获得一项省级上的奖项。
在2018的下半年开学自学了cpp，不过课后练习题做的比较少，所以我选的是个人赛C/C++的程序设计开发.

# 递归与分治的调用 #

在调用一个函数的过程中又出现直接或间接地调用该函数本身，称为函数的递归调用。Ｃ语言的特点之一就在于允许函数的递归调用

下面是一道经典例题
## Hanoi(汉诺塔)问题 ##
![Algorithm_Recursion_Hanoi_problem](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E7%AC%AC%E5%8D%81%E5%B1%8A%E8%93%9D%E6%A1%A5%E6%9D%AF/%E9%80%92%E5%BD%92%E4%B8%8E%E5%88%86%E6%B2%BB%E7%9A%84%E8%B0%83%E7%94%A8/Hanoi%E5%A1%94%E9%97%AE%E9%A2%98/Algorithm_Recursion_Hanoi_problem.png?x-oss-process=style/Hexo)
由上面的分析可知：将ｎ个盘子从Ａ座移到Ｃ座可以分解为以下3个步骤：
1.将Ａ上ｎ－１个盘借助Ｃ座先移到Ｂ座上。
2.把Ａ座上剩下的一个盘移到Ｃ座上。
3.将ｎ－１个盘从Ｂ座借助于Ａ座移到Ｃ座上。

 下面是c语言的描述
 ```C
 #include <stdio.h>
 void main()
 {
   void hanoi(int n,char one,char two,char three);
   int m;
   printf("input the number of diskes:");
   scanf("%d",&m);
   printf("The step to moveing %d diskes: \n",m);
   hanoi(m,'A','B','C');
 }
 void hanoi(int n,char one,char two,char three)
 {
   void move(char x,char y);
   if(n == 1)
   move(one,three);
   else
   {
     hanoi(n-1,one,three,two);
     move(one,three);
     hanoi(n-1,two,one,three);
   }
   void move(char x,char y)
   {
     printf("%c-->%c\n",x,y);
   }
 }
 ```

 ## 求两个字符串中最大公共子序列的长度 ##
例如两个字符串 str1=“abcdefg”与 str2=“hdefghijk”
子序列则是从不改变序列的顺序，而从序列中去掉任意的元素而获得新的序列；
也就是说，子串中字符的位置必须是连续的，子序列则可以不必连续。

1、如果str1与str2的长度为0，则最大序列长度为0；
2、如果str1与str2的第一个字符相等，则继续在str1与str2的其余字符子串中寻找，并长度加1；
F(str1,str2)=f(str1.substring(1),str2.substring(1))+1
3、如果str1与str2的第一个字符不相等，则在str1与str2的其余字符子串
以及 str1的其余字符子串与str2中进行比较，取其中最大值
F(str1,str2)=MAX(f(str1,str2.substring(1)), f(str1.sbstring(1),str2))
