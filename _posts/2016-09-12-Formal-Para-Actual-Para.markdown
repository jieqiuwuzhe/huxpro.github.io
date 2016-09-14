---
layout:     post
title:      "C/C++参数传递详解"
subtitle:   " \"值传递、指针传递、引用传递\""
date:       2016-09-12 14:57:00
author:     "Root"
header-img: "img/contact-bg.jpg"
catalog: true
tags:
    - C++
---

> “当黑色的玫瑰悄悄绽放，除了镜花水月，又有谁，能够了解我的心？————诡术妖姬 ”


## 参数传递

C或C++中函数的参数传递包括：**值传递、指针传递、引用传递** 这三种方法。三种方式效果完全不同：

先看源码：
		
		#inclde <iostream>
		using namespace std;
		void swap(int i, int j) //值传递
		{
			int temp;
			temp = i;
			i = j;
			j = temp;
		}
		void swap1(int *i, int *j) //指针传递
		{
			int temp;
			temp = *i;
			*i = *j;
			*j = temp;
		}
		void swap2(int &i, int &j) //引用传递
		{
			int temp;
			temp = i;
			i = j;
			j = temp;
		}
		int main( ) 
		{
			int a = 1, b = 2;
			cout<<a<<b<<endl;
			swap(a,b);
			//swap1(a,b);
			//swap2(a,b);
			cout<<a<<b<<endl;
		}

以上三种方式执行完之后，结果分别是：

1,2    1,2

1,2    2,1

1,2    2,1

### 值传递

只是传递了参数值，a,b 和 i,j 的地址是不同的，因此改变 i,j 并不影响 a,b 。

### 指针传递

传递的是指针，a,b 的指针被传递给了 i,j ，因此交换成功。

### 引用传递
引用传递时，对形参的操作等同于对实参的操作，即传递的不会是实参的副本，而就是实参。所有操作都是对同一地址进行的操作，故交换成功



—— Root 于 2016.9


