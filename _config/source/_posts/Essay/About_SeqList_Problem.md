---
title: SeqList中的相关API函数问题
date: 2019-08-13 10:55:20
tags: Data Structure
---
# 一、SeqList_Length引发tlist和list的思考
**(一)SeqList_Length01() & SeqList_Length02()的区别和不同是什么?**    
**(二)探究为什么要引入一个(TSeqList *)tlist? 意义何在***

```C
/*
Date:2019-08-13 11:00
Author:Gmrakari
*/
typedef struct _tag_SeqList
{
	int length;
	int capacity;
	unsigned int *node;
}TSeqList;

typedef void SeqList;
typedef void SeqListNode;

int SeqList_Length01(SeqList* list)
{
	TSeqList *tlist = NULL;

	if(list == NULL)
	{
		return -1;
	}

	tlist = (TSeqList *)list;

	return tlist->length;
}

int SeqList_Length02(SeqList* list)
{
	if(list == NULL)
	{
		return -1;
	}
	//第一次编译
	return list->length;; //err:	IntelliSense:  表达式必须包含指向结构或联合的指针类型

	//第二次编译
	//return (TSeqList *)list->length; // IntelliSense:  表达式必须包含指向结构或联合的指针类型
	//一样报错 这样我才意识到 list 是一个没有定义的结构体 typedef void SeqList;是一个空类型

}
```

通过编译，查看错误信息才解释，为什么要引入一个(TSeqList *)tlist变量的原因
需要让list 跟 tlist 绑定，让list 拥有 tlist 的属性
这是属于结构体基础问题，没掌握好基础语法导致的

# 二、SeqList_Insert的位置后移问题
****(一)后移位置的条件是for (i = tlist->length; i < pos; i--)还是for (i = tlist->length; i > pos; i--)?****    
****(二)后移的元素是tlist->node[i + 1] = tlist->node[i]还是tlist->node[i] = tlist->node[i - 1]?****

```C
#define  _CRT_SECURE_NO_WARNINGS
#include<stdio.h>
#include "stdlib.h"
#include "string.h"

typedef struct _tag_SeqList
{
	int length;
	int capacity;
	unsigned int *node;
}TSeqList;
typedef void SeqList;
typedef void SeqListNode;

SeqList* SeqList_Create(int capacity)
{
	TSeqList *tmp = NULL;
	int ret = 0;
	tmp = (TSeqList *)malloc(sizeof(TSeqList));

	if (tmp == NULL)
	{
		ret = -1;
		printf("func SeqList_Create() err:%d", ret);
		return NULL;
	}
	memset(tmp, 9, sizeof(TSeqList));

	tmp->node = (unsigned int *)malloc(sizeof(unsigned int *)*capacity);
	if (tmp->node == NULL)
	{
		ret = -2;
		printf("tmp->node malloc err:%d", ret);
		return NULL;
	}

	tmp->capacity = capacity;
	tmp->length = 0;

	return tmp;
}
int SeqList_Length(SeqList* list)
{
	TSeqList *tlist = NULL;

	if (list == NULL)
	{
		return -1;
	}

	tlist = (TSeqList *)list;

	return tlist->length;
}

int SeqList_Insert(SeqList* list, SeqListNode* node, int pos)
{
	int i = 0;
	TSeqList *tlist = NULL;

	tlist = (SeqList *)malloc(sizeof(TSeqList));

	if (tlist == NULL || list == NULL || pos < 0)
	{
		return -1;
	}

	tlist = (TSeqList *)list;

	if (tlist->length > tlist->capacity)
	{
		return -1;
	}

	if (pos > tlist->length)
	{
		pos = tlist->length;
	}

	//元素后移过程
	//第一次  31 32 33 34 35 35

	//for (i = tlist->length; i < pos; i--)
	for (i = tlist->length; i > pos; i--)
	{
		// err 1 tlist->node[i + 1] = tlist->node[i];
		// err 2 tlist->node[i] = tlist->node[i - 1];
		// tlist->node[i + 1] = tlist->node[i]; 程序断掉
		tlist->node[i] = tlist->node[i -1];
	}

	// 第二次 35 34 33 35 32 31
	// for (i = tlist->length; i > pos; i--)
	// {
	// 	tlist->node[i] = tlist->node[i - 1];//reference a[i] = a[i - i]--->a[7] = a[6]
	// }

	//insert

	tlist->node[i] = (unsigned int)node;
	tlist->length++;

	return 0;
}

SeqListNode* SeqList_Get(SeqList* list, int pos)
{
	int i = 0;
	SeqListNode *ret = 0;
	TSeqList *tlist = NULL;
	if (list == NULL || pos < 0)
	{
		printf("SeqList_Get() err:%d\n", ret);
		return NULL;
	}
	tlist = (TSeqList *)list;

	ret = (void *)tlist->node[pos];
	return ret;
}


typedef struct _Teacher
{
	int age;
	char name[64];
}Teacher;

int main()
{
	int		ret = 0, i = 0;
	SeqList* list = NULL;

	Teacher t1, t2, t3, t4, t5;
	t1.age = 31;
	t2.age = 32;
	t3.age = 33;
	t4.age = 34;
	t5.age = 35;

	list = SeqList_Create(10);
	if (list == NULL)
	{
		printf("func SeqList_Create() ret :%d \n", ret);
		return;
	}
	ret = SeqList_Insert(list, (SeqListNode*)&t1, 0); //头插法
	ret = SeqList_Insert(list, (SeqListNode*)&t2, 0); //头插法
	ret = SeqList_Insert(list, (SeqListNode*)&t3, 0); //头插法
	ret = SeqList_Insert(list, (SeqListNode*)&t4, 0); //头插法
	ret = SeqList_Insert(list, (SeqListNode*)&t5, 0); //头插法
	ret = SeqList_Insert(list, (SeqListNode*)&t5, 2);

	//遍历
	for (i = 0; i < SeqList_Length(list); i++)
	{
		Teacher*  tmp = (Teacher *)SeqList_Get(list, i);
		if (tmp == NULL)
		{
			return;
		}
		printf("tmp->age:%d ", tmp->age);
	}

	system("pause");
 }
```
把所有代码贴出来，方便直接在机器上运行
主要看79-99行

```C
for (i = tlist->length; i < pos; i--)
{
	tlist->node[i + 1] = tlist->node[i];// err 1
	tlist->node[i] = tlist->node[i - 1];// err 2
	tlist->node[i + 1] = tlist->node[i];// 程序断掉
}

i<pos;这样程序没有结束条件了 就是任何时候都可以成立，比如i = 1 ;1 < pos; i = 0, 0 < pos;
所以是 i > pos; 后移tlist->length - pos - 1 次
tlist->node[i + 1] = tlist->node[i];// 程序断掉
这个很好理解，当i = tlist->length时,i + 1 数组越界，程序出错
```
下面还有一张帮助理解的图
![SeqList_Insert.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/Data_Structure/SeqList_Insert.png?Expires=1566617680&OSSAccessKeyId=TMP.hV8XmGvTtLXA5gbqHoCmMutPShAiqBfH2AePb8q6vtKP2NMdss9PiLVaQpKhyfsLgR61ZjkrvtdL3xL3u2iG4eLfzS2TbSvxEUxkmrumiWxkdYfRCxb8KiovQpKm56.tmp&Signature=tx5qmnS3yH8f%2B9NqTXflbR%2Fj9hc%3D)

总结，任何时候，将遇到的问题先编译一遍，查看报错信息，然后进行分步调试，必要时候，在纸上跟着程序模拟走，当程序出错的时候，分析错误原因，这样才能将遇到的问题迎刃而解。
