---
title: 偶遇朋友圈上的字符串反转问题
date: 2018-12-24 13:45:20
tags: 字符串数组
---

# 到底是怎么实现的 #
我已经50天左右没看朋友圈了，突然这几天想发个动态什么的 就打开了朋友圈的入口 发现今日的朋友圈都是吃喝玩乐 还有些炫狗的 我还是选择不发了 然后关闭 花更多的时间玩一些与编程有关的东西，但是这次打开朋友圈 却有意外的收获 所以才会有这篇文章
就是今天让我研究的一个问题:字符串的反转
看下面这张图的描述
![The_problem_description](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%8F%8D%E8%BD%AC/The_problem_description.jpg?x-oss-process=style/Hexo)
这张图片还挺有意思的，因为我觉得反转这些字母很简单，让我来实现的话，就是把那串字母复制到编好的程序里面，一个Enter键就出来了。但是难点就是在这，这个程序怎么实现？我就是为了解决这个问题而来的。很不爽的就是，自己打代码想要实现的时候，错误百出（肯定是以前眼高手低造成的），导致基础薄弱，产生了很多令自己很无奈的bug。
需求阐述：把字母反转过来
由于我之前学过扫地僧老师讲过的项目开发中字符串模型——字符串反转模型
理解递归的2个重要点
1、参数的入栈模型
2、函数嵌套调用返回流程
这个内容好像都有半年了，现在只剩下一点点印象，具体怎么实现，还是很懵逼。然后查看了相关资料，觉得这三个最具有帮助
[1、Youtube—Java实现常见对象字符串反转的案例](https://www.youtube.com/watch?v=GX2aCYiOvcg)
[2、程序园-通过运用指针将字符串反转](http://www.voidcn.com/article/p-pmldbayd-kt.html)
[3、程序园-递归实现字符串反转](http://www.voidcn.com/article/p-ybmaathr-kt.html)

我说说我的想法：
1、输入一个数组 然后遍历输出这个数组的内容
2、通过翻转数组，反过来输出这个数组的内容

```C
#define  _CRT_SECURE_NO_WARNINGS
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
int main()
{
  char str1[1024];
	char *str2;
	str2 = gets(str1);
	int length = strlen(str2);
	char str3[] = "";
	int i;
	int j = 0;
	for (i = length - 1; i >= 0; i--)
	{
		str3[j] += str2[i];
		j++;
	}
	str3[length] = '\0';
	for (j = 0; j <= length - 1; j++)
	{
		printf("str3:%c", str3[j]);
	}
	system("pause");
}
```

我写出来的东西实现不了，我到底错在哪里？最后我将str3,str3[j],str2这三个变量加入监听，然后调啊调，终于让我找到了。我在调试窗口看到这句`str3[length] = '\0';`出现烫烫烫烫什么的字符。意味着我定义的这个char str3并没有结束语句，然后通过改成	`str3[j] = '\0';`问题是，我为什么要这样改？因为我想到，它在最后一个字母上添加'\0',这样才能标志着字符结束。
![without_add_0](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%8F%8D%E8%BD%AC/without_add_0.png?x-oss-process=style/Hexo)
结果能出得来，但是程序还是会断掉，问题我暂时找不出来，那先放一放，以后再深究。
![success_program](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%8F%8D%E8%BD%AC/success_program.png?x-oss-process=style/Hexo)

这个是扫地僧老师教的方法，可以拿去测试，没有问题的。
```C
#define  _CRT_SECURE_NO_WARNINGS
#include <stdlib.h>
#include <string.h>
#include <stdio.h>
void main()
{
	char buf[] = "abcdefg";
	int length = strlen(buf);
	char *p1 = buf;
	char *p2 = buf + length -1;//指向末尾

	while(p1<p2)
	{
		char c = *p1;
		*p1 = *p2;
		*p2 = c;
		++p1;
		--p2;
	}
	printf("buf:%s",buf);
	system("pause");
	return 0;
}
```
想到期末要考数据库原理，还是花多点时间去复习一下(准确的来说,我应该是从头到尾学一遍,因为上课都没有听过,现在想起来很有愧疚感)，抓紧时间过一遍，万一我把查询的知识点都掌握了呢？
