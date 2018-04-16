---
layout:     post   				    # 使用的布局（不需要改）
title:      洛谷1187题解 				# 标题 
subtitle:   算法的世界           #副标题
date:       2018-04-17			# 时间
author:     LYC					# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags: 模拟

---

[洛谷1187](https://www.luogu.org/problemnew/show/P1187)

## 分析
- 首先考察简单情况，如果只有两个在一起的立方体，那末会减少2个面。
- 受此启发，猜想每有两个靠在一起的立方体，就会减少2面。
- 减面数的时候是以每个立方体6面为基础减的。
- 本题中为了叙述方便，我们认为相邻的两立方体是有*联系*的。
- 联系具有*方向性*。譬如A->B与B->A是不同的联系。
- 联系数等于减少的面数，读者自证不难。

## 做法
- 遍历统计即可。

### 优化
- 注意到由于重力作用，不可能出现空中阁楼，所以竖直方向的统计可以通过坐标运算在常数时间里解决。

代码如下：

```
#include<cstdio>
#define MAXN 1005

int n,m,total,s,rep;
int a[MAXN][MAXN];
int dir[4][2]={{-1,0},{0,1},{1,0},{0,-1}};
void prework(){s=6*total;s-=rep;rep=0;}

inline bool clear()
{
    bool ok=false;
    for(int i=1;i<=n;i++)
    for(int j=1;j<=m;j++)
    {
        if(a[i][j])a[i][j]--;
        if(a[i][j])ok=true;
    }
    return ok;
}
inline bool judge(int x,int y)
{
    if(x<1||x>n)return true;
    if(y<1||y>m)return true;
    return false;
}

void input();
int search();
int main()
{
    input();
    prework();
    //一层一层地处理 
    do
    {
        rep=0;
        s-=search();
    } while(clear());
    //如果仍然有方块就继续执行 
    printf("%d",s);
    return 0;
}

void input()
{
    scanf("%d%d",&n,&m);
    for(int i=1;i<=n;i++)
    for(int j=1;j<=m;j++)
    {
        scanf("%1d",&a[i][j]);
        total+=a[i][j];
        if(a[i][j])rep+=2*(a[i][j]-1);
    }
}

int search()
{
    for(int x=1;x<=n;x++)
    for(int y=1;y<=m;y++)
    {
        if(a[x][y])
        for(int direc=0;direc<=3;direc++)
        {
            int nx=x+dir[direc][0];
            int ny=y+dir[direc][1];
            if(judge(nx,ny))continue;
            if(a[nx][ny])rep++;
        }
    }
    return rep;
}
```

> END
