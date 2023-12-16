---

title: 队列
tags: [队列,C语言,data-structure]
categories: [413J-数据结构]
description: 进入文章

---

---


### 队列

```c
/*
	时间：2021年10月4日14:22:12 
	编程目标： 
			针对循环队列，设计顺序队列的
			入队和出队的算法 

*/ 
# include <stdio.h>
# include <malloc.h>

//结构定义
# define MAXSIZE 10
# define ElemType int 
typedef struct 
{
	ElemType elem[MAXSIZE];
	int rear ,front;
} SeQueue;


//(1)置空队
SeQueue * InitSeQueue( )
{ 
	SeQueue * q=( SeQueue* )malloc( sizeof( SeQueue));
	q->front =q->rear= MAXSIZE-1;
	
	return q;
}

//(2)入队
int InSeQueue( SeQueue * q, ElemType x)
{
	if((q->rear+1)% MAXSIZE==q->front) //队满不能入队
		{
			printf("队满");
			return 0 ;
		}
	else
		{
			q->rear=(q->rear+1)%MAXSIZE;
			q->elem[q->rear]=x;
			return 1; //入队完成
		}
}

//(3)出队
int OutSeQueue( SeQueue *q,ElemType * x)
{  if(q->front==q->rear)
	{
		printf("队空");
		return 0;
	}
	else
	{
		q->front=(q->front+1)% MAXSIZE;
		*x=q->elem[q->front]; //读出队头元素
		return 1; //出队完成
	}
	
}
//判断队列空 
int EmptySeQueue( SeQueue * q)
{ 
	if(q->front==q->rear) 
		return 1;
	else 
		return 0;
}
	
	
int main (void)
{
	//定义指向队列的指针
	int x;
	SeQueue * sq =InitSeQueue( );
	
	// 置空队
	if(sq!=NULL)
	 	printf("置空队成功！\n");
	
	//入队
	printf("请输入需要入队的元素: \n");
	scanf("%d",&x);
	if(1 == InSeQueue(sq, x))
			printf("入队成功！\n");
	else
			printf("入队失败！\n");

	
	//出队
	printf("进行出队！ \n");
	if(1 ==OutSeQueue( sq,&x))
			printf("出队成功！出队元素：%d\n",x);
	else
			printf("出队失败！\n");
	
			
	return 0 ;
} 		
	
	

```


---

> Citation:
> - []()
> 
> References:
> - []()
