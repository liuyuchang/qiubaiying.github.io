---
layout:     post   				    # 使用的布局（不需要改）
title:      洛谷1803题解 				# 标题 
subtitle:   算法的世界           #副标题
date:       2018-04-30			# 时间
author:     LYC					# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags: 贪心

---

## 题目背景

快noip了，yyy很紧张！

## 题目描述

现在各大oj上有n个比赛，每个比赛的开始、结束的时间点是知道的。

yyy认为，参加越多的比赛，noip就能考的越好（假的）

所以，他想知道他最多能参加几个比赛。

由于yyy是蒟蒻，如果要参加一个比赛必须善始善终，而且不能同时参加2个及以上的比赛。

## 输入输出格式

### 输入格式：

第一行是一个整数n ，接下来n行每行是2个正整数ai,bi(ai<bi)，表示比赛开始、结束的时间。

### 输出格式：

一个整数最多参加的比赛数目。

### 输入输出样例

输入样例#1：

3

0 2

2 4

1 3

输出样例#1：

2

说明

对于20%的数据，n≤10；

对于50%的数据，n≤1000；

对于70%的数据，n≤100000；

对于100%的数据，n≤1000000，0≤ai＜bi≤1000000。

----------

## 分析(来自kkksc03)

> 在一个数轴上有n条线段，现要选取其中k条线段使得这k条线段两两没有重合部分，问最大的k为多少。

> 最左边的线段放什么最好？

> 显然放右端点最靠左的线段最好，从左向右放，右端点越小妨碍越少

> 其他线段放置按右端点排序，贪心放置线段，即能放就放。

## 编程实现

用一个结构体去实现好了，另外快排一下就好了，不难。

代码：

```

#include<stdio.h>
#include<algorithm>
#define MAXN 1000005
#define HOME
#define TEST printf("a test.\n")
using namespace std;

struct node
{
    int front;
    int rear;
};
node a[MAXN];

bool cmp(node x,node y)
{
    return (x.rear<y.rear);
}


int main()
{
#ifdef NOIP
    freopen(".in","r",stdin);
    freopen(".out","w",stdout);
#endif
    
    int n;
    scanf("%d",&n);
    
    for(register int i=1;i<=n;i++)
    {
        scanf("%d%d",&a[i].front,&a[i].rear);
    }
    sort(a+1,a+1+n,cmp);
    
    int ocrupy=-1,sum=0;
    for(register int i=1;i<=n;i++)
    {
        if(a[i].front>=ocrupy){
            sum++;
            ocrupy=a[i].rear;
        }
        else continue;
    }
    
    printf("%d",sum);
    
    return 0;
}
```

*END*
