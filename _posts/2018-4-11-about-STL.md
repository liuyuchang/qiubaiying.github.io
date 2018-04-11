---
layout:     post   				    # 使用的布局（不需要改）
title:      关于STL你应该知道的 				# 标题 
subtitle:   算法的世界 #副标题
date:       2018-04-11			# 时间
author:     LYC					# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags: NOTE
---

## 前言
1. STL是个挺重要的东西，然而知识比较杂，有些细节也不大好弄。
2. CCF的书粗略地讲了讲；一本通连提都没提。关于STL，刘汝佳的书上是这么说的：“ *把本章内容看作是可选的工具，如果某些工具难以掌握，索性避开就是了。*”
3. 然而关键是，**刘汝佳的书后面全是用STL !!!**

-----------

### 本文章的资料来自：
1. 刘汝佳的《算法竞赛入门经典(第二版)》
2. CCF的某系列书
3. 北大教授郭某的MOOC课程
4. google & 百度 上的各种资料

-----------

## 一、栈(stack)


------------

## 二、向量(vector)


------------

## 三、排列
### *pre_permutation & next_permutation*


------------
## 四、快速排序(sort)
**以下是快速排序的实现细节。建议编程时使用STL，但一定要搞懂细节(代码来自于[洛谷](https://www.luogu.org/record/show?rid=3483442))**
```
#include<bits/stdc++.h>
using namespace std;
int a[100000+10];
void SORT(int l,int r)
{
    int mid=a[(l+r)/2];
    int i=l,j=r;
    while(i<=j)
    {
        while(a[i]<mid)i++;
        while(a[j]>mid)j--;
        if(i<=j)
        {
            swap(a[i],a[j]);i++;j--;
        }
    }
    if(i<r)SORT(i,r);
    if(j>l)SORT(l,j);
}

int main()
{
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        cin>>a[i];
    }
    SORT(1,n);
    for(int i=1;i<=n;i++)
    {
        cout<<a[i]<<" ";
    }
    return 0;
}

```
- sort()是一个很重要的函数，你可以很方便地用它对数据排序。
- 如果sort(  ,  )中只有两个参数，默认从小到大排序。参数是两个指针，指向一段连续的区间，左闭右开。

**两个参数的情况非常简单，可以参考实例[2006年NOIP的一道水题](https://www.luogu.org/problemnew/show/P1059)**

- sort()可以对自定义的数据类型排序，做法是传入一个比较函数。直接看实例[P1781 宇宙总统](https://www.luogu.org/problemnew/show/P1781)，比较好理解。

```
#include<bits/stdc++.h>
using namespace std;
struct paiming
{
    string num;
    int index;
}a[25];
bool cmp(paiming x,paiming y)
{
    if(x.num.size()!= y.num.size())
    return x.num.size()>y.num.size();
    return x.num>y.num;
}
int main()
{
    int n;
    cin>>n;
    for(int i=1;i<=n;i++)
    {
        cin>>a[i].num;
        a[i].index=i;
    }
    sort(a+1,a+1+n,cmp);
    cout<<a[1].index<<endl<<a[1].num;
    return 0;
}
```
- cmp是**比较**的意思，在bool cmp(paiming x,paiming y)函数中，**return x.num>y.num;**的意思是当x.num>y.num时**x排在y的前面**。
- sort()**不可对二维数组或是高维数组排序**，但这并不会影响它的实用性。我们可以通过结构体的方式存储数据，传入比较函数，同样可以使用sort()进行排序。参考[2002年上海省选某题的递推做法](https://www.luogu.org/problemnew/show/P1434)

```
#include<cstdio>
#include<algorithm>
using namespace std;
const int MAXN=105;
int r,c;
struct node
{
    int x,y;
    int sum;
    int l;
}a[MAXN*MAXN];
bool cmp(node j,node c)
{ 
    return j.sum < c.sum ;
}
inline void input()
{
    scanf("%d%d",&r,&c);
    for(int i=1;i<=r;i++)
    for(int j=1;j<=c;j++)
    {
        a[c*(i-1)+j].l =1;
        a[c*(i-1)+j].x =i;
        a[c*(i-1)+j].y =j;
        scanf("%d",&a[c*(i-1)+j].sum);
    }
}
inline bool judge(int zxx,int k)
{
    if(abs(a[zxx].x-a[k].x)==1&&abs(a[zxx].y-a[k].y)==0)return true;
    if(abs(a[zxx].x-a[k].x)==0&&abs(a[zxx].y-a[k].y)==1)return true;
    return false;
}
int main()
{
    input();
    sort(a+1,a+1+r*c,cmp);
    int max_play_len=0;
    for(int k=1;k<=r*c;k++)
    {
        int max_len=0;
        for(int zxx=k-1;zxx>=1;zxx--)
        {
            if(zxx==0)break;
            if(judge(zxx,k)&&a[zxx].l>max_len&&a[zxx].sum<a[k].sum)max_len=a[zxx].l;
        }
        a[k].l+=max_len;
        if(a[k].l>max_play_len)max_play_len=a[k].l;
    }
    printf("%d",max_play_len);
    return 0;
}
```

- 关于sort()的更多用法请参考：
[百度百科](https://baike.baidu.com/item/sort%28%29/13475541?fr=aladdin) or [维基百科](
https://en.m.wikipedia.org/wiki/Sort_(C%2B%2B))

------------
## 五、二分查找
### *binary_search & lower_bound & upper_bound*

------------

## 六、队列(queue) & 优先队列


-------------

## 七、映射(map)


--------------

## 八、集合(set)


--------------
## 九、*max_element & min_element*

