---
layout:     post   				    # 使用的布局（不需要改）
title:      洛谷1051题解 				# 标题 
subtitle:   算法的世界 #副标题
date:       2018-04-16			# 时间
author:     LYC					# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:  模拟

---

[洛谷1051](https://www.luogu.org/problemnew/show/P1051)

本来这是一道水题，但看到题解里很多用排序做的，感到十分捉急。

## 这题并不需要排序，只要边读边处理就好了。

- 读入的时候每读一组数据，就计算获得的奖学金。
- 如果这组数据的奖学金比之前记录的要大，记录之。同时记录学生的编号。
- 同时用一个全局变量记录奖学金总数。
- 输出即可。

代码如下：
```
#include<stdio.h>
#include<iostream>
#include<cstring>
#define HOME
using namespace std;

int n,pre=-1,ans=-1,sumup;
struct node
{
    char c[25];
    int score_exam,
        score_class;
    char leader;
    char province;
    int sum_paper;
}a[105];

 inline void input()
{
    scanf("%d",&n);
    for(int i=1;i<=n;i++)
    {
        int total=0;
        scanf("%s",a[i].c);
        scanf("%d%d",&a[i].score_exam,&a[i].score_class);
        cin>>a[i].leader;
        cin>>a[i].province;
        scanf("%d",&a[i].sum_paper);
        
        if(a[i].score_exam>80&&a[i].sum_paper>=1)total+=8000;
        if(a[i].score_exam>85&&a[i].score_class>80)total+=4000;
        if(a[i].score_exam>90)total+=2000;
        if(a[i].score_exam>85&&a[i].province=='Y')total+=1000;
        if(a[i].score_class>80&&a[i].leader=='Y')total+=850;
        
        sumup+=total;
        
        if(total>pre){
            pre=total;
            ans=i;
        }
    }
    
}

int main()
{
#ifdef NOIP
    freopen(".in","r",stdin);
    freopen(".out","w",stdout);
#endif
    input();
    
    printf("%s\n",a[ans].c);
    printf("%d\n",pre);
    printf("%d\n",sumup);
    
    return 0;
}
```
> END
