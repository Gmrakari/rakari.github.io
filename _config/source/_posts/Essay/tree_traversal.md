---
title: 树的遍历问题
date: 2018-10-02 14:29:21
tags: Data Structure
---

# 树的遍历（文末附有C语言实现方法） #

因为要复习，顺便把这个贴出来，以便应急之需，但是文字可能比较蹩脚
刚开始学树的遍历的时候，遇到很多瓶颈，但是只能通过看csdn里面的例题，况且那些资料又不统一，导致要理解花费太多时间，现在为了减少后学者遇到的麻烦，我这里详细说下怎么解树的遍历问题

一般有两种形式：
1、已知先序遍历和中序遍历——求后序遍历
2、已知中序遍历和后序遍历——求先序遍历
我先总结一下两种形式的方法，后面再详细用我的课本里面的习题讲解
**不管是哪种方法，都是需要先找到树的根**
前+中 ：在前序中第一个就是根
后+中：后序遍历中最后一个结点都是根，一层一层往上找

如果上面这两句不明白的话，我们继续用我在校使用教材的一道课后练习题来解释一下
## 已知先序遍历和中序遍历——求后序遍历 ##
**题目：已知一棵树的先序遍历是ABDCEFG,中序遍历是BDACFEG，则该二叉树的后序遍历是?**
解析:
先序ABDCEFG
中序BDACFEG
第一轮我们在先序中找到A就是树的根，根据中序，我们就知道BD是A的左子树，CFEG是右子树
![Know_DLR&LDR_get_LRD_first_round.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_DLR%26LDR_get_LRD_first_round.png)

先序BD CEFG
中序 BD CFEG
第二轮我们在先序找到B,C为根结点；根据中序，我们就知道D为B的右子树（B的左边没有结点），FEG为C的右子树（C的左边也没有结点），这样我们的确定
![Know_DLR&LDR_get_LRD_second_round.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_DLR%26LDR_get_LRD_second_round.png)

先序 EFG
中序 FEG
第三轮我们就回到了刚开始的情形，就是用递归的方法，重新将剩下的结点遍历一次,在先序中找到E为根，然后根据中序，我们知道F是E的左子树，G是E的右子树。最后我们就可以还原了树的形状。然后我们就知道这棵树的后续遍历是DBFGECA
![Know_DLR&LDR_get_LRD_third_round.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_DLR%26LDR_get_LRD_third_round.png)
## 已知中序遍历和后序遍历——求先序遍历 ##

**题目:已知一棵树的中序遍历DHEBAFGC,后序遍历是DHEBGFCA,则该二叉树的先序遍历是?**
解析:
中序DHEBAFGC
后序DHEBGFCA
首先第一轮我们在后序遍历中找到最后一个结点是A，所以A就是这颗树的根。然后根据中序，我们就知道DHEB是A的左子树，FGC是A的右子树
![Know_LDR&LRD_get_DLR_first_round.png](https://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_LDR%26LRD_get_DLR_first_round.png)
中序DHEB		FGC
后序DHEBGFC
第二轮我们在后序遍历中找到A的左右子树的根结点为B和C（最后一个结点），然后根据中序遍历，我们知道DHE为B的左子树，FG为C的左子树。
![Know_LDR&LRD_get_DLR_second_round.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_LDR%26LRD_get_DLR_second_round.png)
中序 DHE		FG
后序DHE 		GF
第三轮我们在后序遍历中找到E，F为根结点，然后根据中序遍历，我们就知道DH为E的左子树，G为F的右子树。
![Know_LDR&LRD_get_DLR_third_round.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_LDR%26LRD_get_DLR_third_round.png)
中序DH
后序DH
第四轮我们在后序遍历中找到H为根结点，然后根据中序遍历，我们知道D为H的左子树
最后我们根据树的图，得到树的先序遍历为ABEHDCFG
![Know_LDR&LRD_get_DLR_fourth_round.png](http://couldpic.oss-cn-beijing.aliyuncs.com/hexo/%E6%A0%91%E7%9A%84%E9%81%8D%E5%8E%86/Know_LDR%26LRD_get_DLR_fourth_round.png)

```C
#include<stdio.h>
#include<string.h>
#include<malloc.h>
typedef struct Node {
    char a;
    struct Node *lchild;
    struct Node *rchild;
}BiNode, *BiTree;

void PosTraverse(BiTree T)
{
    if (T == NULL) return;
    PosTraverse(T->lchild);
    PosTraverse(T->rchild);
    printf("%c", T->a);
}
void BuildTree(char *pre, char* mid, BiTree root) {
    int len = strlen(pre);
    if (0 == len)
    return;
    char *p = strchr(mid, pre[0]);
    int pos = p - mid;
    root->a = pre[0];
    root->lchild = root->rchild = NULL;
    if (pos != 0) {
        BiTree left;
        root->lchild = (BiTree)malloc(sizeof(BiNode));
        left = root->lchild;
        char *left_pre = (char*)malloc(sizeof(char) * (pos + 1));
        char *left_mid = (char*)malloc(sizeof(char) * (pos + 1));
        strncpy(left_pre, pre + 1, pos);
        strncpy(left_mid, mid, pos);
        left_pre[pos] = 0;
        left_mid[pos] = 0;
        BuildTree(left_pre, left_mid, left);
    }
    if (pos != len - 1) {
        BiTree right;
        root->rchild = (BiTree)malloc(sizeof(BiNode));
        right = root->rchild;
        char *right_pre = (char*)malloc(sizeof(char) * (len - pos));
        char *right_mid = (char*)malloc(sizeof(char) * (len - pos));
        strncpy(right_pre, pre + 1 + pos, len - pos - 1);
        strncpy(right_mid, mid + 1 + pos, len - pos - 1);
        right_pre[len - pos - 1] = 0;
        right_mid[len - pos - 1] = 0;
        BuildTree(right_pre, right_mid, right);
    }
}

int main() {
    BiNode temp;
    BuildTree("abdcefg", "bdacfeg", &temp);
    PosTraverse(&temp);
}

```
