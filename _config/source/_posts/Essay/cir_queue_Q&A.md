---
title: 循环队列
date: 2018-10-02 17:44:17
tags: [Data Structure,Q & A]
---
I have some puzzled about queue.
For instance,what does "Q->front = (Q->front+1) %MAXLEN"mean in EnCQueue & OutCQueue opeartion mean?
I have referenced code from
[The Learnming Point](http://www.thelearningpoint.net/computer-science/data-structures-queues--with-c-program-source-code)
[CSDN:Daydream Mr](https://blog.csdn.net/z498596750/article/details/79375945)

The author on csdn disscuss about queue ,he mentioned that the condition of queue is (rear+1) % QueueSize==front and calc the length of queue principle is (rear->front+QueueSize) % QueueSize,both of the formula that we only could memorization it which make me feel plain while i do not comprehend it.
Ya,that was not explain my question,i trying to understand Q->front = (Q->front+1),however the last part %MAXLEN that i do not konw what %MAXLEN funtion.
Here i pasted the code.     
```C
#include <stdio.h>
#include <stdlib.h>
#include <malloc.h>
#define MAXLEN 100

typedef int DataType;
typedef struct{
    DataType queue[MAXLEN];
    int front,rear;
}SeQueue;

void InitCSeQueue(SeQueue *Q){
    Q->front =Q->rear = -1;
}

int EnCQueue(SeQueue *Q,DataType x)
{
    if(Q->front == (Q->rear +1)%MAXLEN){
        printf("Queue is full,can not enqueue");
        return 0;
    }
    Q->rear = (Q->rear+1)%MAXLEN;
    Q->queue[Q->rear] = x;
    return 1;
}

int OutCQueue(SeQueue *Q,DataType *x){
    if(Q->front == Q->rear){
        printf("Queue is empty,can not outqueue");
        return 0;
    }
    Q->front = (Q->front+1)%MAXLEN;
    *x = Q->queue[Q->front];
    return 1;
}

int GetCQueueHead(SeQueue *Q,DataType *x)
{
    if(Q->front == Q->rear){
        printf("queue is empty,can not empty");
        return 0;
    }
    *x = Q->queue[Q->front+1];
    return 1;
}

void main()
{
    int data;
    SeQueue *Q=(SeQueue *)malloc(sizeof(SeQueue));
    InitCSeQueue(Q);
    EnCQueue(Q,1);
    EnCQueue(Q,2);
    EnCQueue(Q,3);
    EnCQueue(Q,4);
    OutCQueue(Q,&data);
    printf("%d\n",data);
    OutCQueue(Q,&data);
    printf("%d\n",data);
    OutCQueue(Q,&data);
    printf("%d\n",data);
}

```
