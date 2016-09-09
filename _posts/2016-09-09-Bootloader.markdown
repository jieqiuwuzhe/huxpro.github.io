---
layout:     post
title:      "Bootloader开发"
subtitle:   " \"一个简单的Bootloader开发流程\""
date:       2016-09-09 07:45:00
author:     "Root"
header-img: "img/post-bg-rwd.jpg"
catalog: true
tags:
    - 单片机
---

> “我只是部落遗子，你却是高贵公主。我愿把我生命的力量化为三刀为你而战，只为证明我——配的上你。———— 蛮族之王 ”


## 开发Bootloader

### 什么是Bootloader

Bootloader其实也是一段普通的程序，只不过该程序的起始地址是确定的O地址，单片机每次上电都会从这里开始执行，也就是说每次上电后都会先执行Bootloader程序。

### Bootloader要做什么

Bootloader其实可以什么都不做，只是单纯的跳转到应用程序所在地址就可以。

		void Boot_Jump(uint32_t sp,uint32_t pc)
		{
			(void) sp;

			(void) pc;

			__asm("msr msp, r0"); //Set new MSP, PSP based on SP (r0)

			__asm("msr psp, r0"); //Set new MSP, PSP based on SP (r0)

			__asm("mov pc, r1"); //Jump to PC (r1)
		}

也可以在该程序中添加你所需要的外设初始化、计时溢出处理等各种功能。

## 程序升级

### 程序升级流程

一个简单的程序升级流程，只需要将程序文件通过串口、无线、GPRS等等各种方式传入到单片机内部，对该数据块进行校验无误后，即可调用CM3内核的软件重启函数，重启后重新
进入Bootloader，在Bootloader中添加升级程序的检验位，检验到新程序后即利用单片机内部Flash的擦写功能，擦除原程序，写入新程序。


—— Root 于 2016.8


