---
layout:     post
title:      "彻底搞懂C语言回调函数"
subtitle:   " \"人外有人，天外有天\""
date:       2016-08-30 07:45:00
author:     "Root"
header-img: "img/post-bg-rwd.jpg"
catalog: true
tags:
    - C语言
---

> “只有飞速的旋转,才可以止住我的泪水,忘记你的模样。 -不祥之刃。 ”


## 什么是回调函数CallBack

### 回调函数

编程分为两类：系统编程（system programming）和应用编程（application programming）。所谓系统编程，简单来说，就是编写**库**；而应用编程就是利用写好的各种库来编写具某种功用的程序，也就是**应用**。系统程序员会给自己写的库留下一些接口，即API（application programming interface，应用编程接口），以供应用程序员使用。所以在抽象层的图示里，库位于应用的底下。

当程序跑起来时，一般情况下，应用程序（application program）会时常通过API调用库里所预先备好的函数。但是有些库函数（library function）却要求应用先传给它一个函数，好在合适的时候调用，以完成目标任务。这个被传入的、后又被调用的函数就称为**回调函数**（callback function）。
![callback](https://pic1.zhimg.com/0ef3106510e2e1630eb49744362999f8_b.jpg)

也就是说，回调是一个高层调用底层，底层反过来再调用高层的过程。

## 为什么要用回调函数
在回调中，我们利用某种方式，把回调函数像参数一样传入中间函数（这里的中间函数指的是被上层调用，然后又调用回调函数的中间函数）。可以这么理解，在传入一个回调函数之前，中间函数是不完整的。换句话说，程序可以在运行时，通过登记不同的回调函数，来决定、改变中间函数的行为。这就比简单的函数调用要灵活太多。

一个简单的回调函数：
		#include <stdio.h>
 
		void printWelcome(int len)
		{
			printf("欢迎欢迎 -- %d/n", len);
		}
 		
		void printGoodbye(int len)
		{
			printf("送客送客 -- %d/n", len);
		}
		//		
 		void callback(int times, void (* print)(int))
 		{
 			int i;
       		for (i = 0; i < times; ++i)
       		{
            	print(i);
        	}
       		printf("/n我不知道你是迎客还是送客!/n/n");
		}
		
		void main(void)
		{
       		callback(10, printWelcome);
       		callback(10, printGoodbye);
       		printWelcome(5);
		}




## PS

未完待续~~


—— Root 于 2016.8


