---
layout:     post   				    # 使用的布局（不需要改）
title:      逆波兰表达式 				# 标题 
subtitle:   算法的世界 #副标题
date:       2018-05-12			# 时间
author:     LYC					# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:  递归

---


## 题目描述

逆波兰表达式是一种把运算符前置的算术表达式，例如普通的表达式2 + 3的逆波兰表示法为+ 2 3。逆波兰表达式的优点是运算符之间不必有优先级关系，也不必用括号改变运算次序，例如(2 + 3) * 4的逆波兰表示法为* + 2 3 4。本题求解逆波兰表达式的值，其中运算符包括+ - * /四个。

## 输入输出

输入为一行，其中运算符和运算数之间都用空格分隔，运算数是浮点数。

输入为一行，其中运算符和运算数之间都用空格分隔，运算数是浮点数。

## 样例输入输出
```
* + 11.0 12.0 + 24.0 35.0
1357.000000
```

## 提示
可使用atof(str)把字符串转换为一个double类型的浮点数。atof定义在stdlib.h中。

## 碎碎念
题目来源于GGF，难度居然被评为十级。。。话说[GGF的题库](http://oj.noi.cn/oj/#main/home)题解都不需要审核的。。。

## 逆波兰表达式的递归定义

- 不难发现逆波兰表达式的定义是递归的：

1.  一个数是一个逆波兰表达式，值为该数。

2.  “运算符  逆波兰表达式  逆波兰表达式”  是逆波兰表达式，值为两个逆波兰表达式的值的运算的结果。

## 分析

- 既然逆波兰表达式是递归定义的，就可以用递归的形式解决该问题。

- 数据在输入的时候即具有自相似的特点，为什么不在输入的时候就是使用递归函数来进行呢？

## 代码
```
//每一个不曾AC的日子都是一种遗憾 
#include<stdio.h>
#include<iostream>
#include<stdlib.h>
#define HOME
using namespace std;

double exp()
{
	char s[20];
	cin>>s;
	switch(s[0]){
		case '+':return exp()+exp();
		case '-':return exp()-exp();
		case '*':return exp()*exp();
		case '/':return exp()/exp();
		default :return atof(s);
	}
}

int main()
{
#ifdef NOIP
	freopen(".in","r",stdin);
	freopen(".out","w",stdout);
#endif
	
	printf("%lf",exp());
	
	return 0;
}
```

> END

