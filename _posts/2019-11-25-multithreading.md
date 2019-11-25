---
layout: post
title: ios 进程与线程的区别
description: "线程与进程"
tags: [sample post]
image:
background: triangular.png
---

## 什么是进程
	1. 进程是指在系统中正在运行的一个应用程序
	2. 每个进程是独立的，每个进程均运行在其专用且受保护的内存空间内
例如: qq QQ音乐 等单独运行的应用程序

##  什么是线程序
	1. 一个进程下想要执行程序就必须有一个线程（至少有一个，比如 :开发中的：main 线程）
	2. 一个进程的所有任务必须在线程中进行（qq 聊天  qq 音乐放音乐）
###  线程的串行
	1. 一个线程的任务执行是串行的
	2. 如过在一个线程中执行多个任务，那么只能一个一个的按顺序执行这些任务
	3. 也就是说在同一时间内只能执行1个任务
### 什么是多线程
	1.每个进程可以开多个线程，没条线程可以并行（同时）执行不同的任务 （进程->车间 ,线程->车间工人）
	2.多线程技术可以提高开发执行效率（弊端：消耗电）
### 多线程原理
	1.同一时间一个CPU只能处理一个线程
	2.多线程并发（同时）执行，就是一个CPU快速的在多条线程之间调度
### 多线程优点
	1.能够提高任务的执行效率
	2.适当的提高CPU和内存的使用率
### 多线程缺点
	1.创建线程是有开销的，iOS下主要成本包括：内核数据结构（大约1KB）、栈空间（子线程512KB、主线程1MB，也可以使用-setStackSize:设置，但必须是4K的倍数，而且最小是16K），创建线程大约需要90毫秒的创建时间

##多线程在iOS开发中的应用
	1.一个iOS程序运行后，默认会开启1条线程，称为“主线程”或“UI线程”（系统设计有关系，所有和UI有关系的都在主线程中做，可以在子线程做，会出问题，官方文档建议）
	2.刷新 或者UI界面
	3.处理UI事件（比如点击事件、滚动事件、拖拽事件等）
## 主线程的使用注意
	1.别将比较耗时的操作放到主线程中
	2.耗时操作会卡住主线程，严重影响UI的流畅度，给用户一种“卡”的坏体验

## 测试demo
<div xmlns:cc="http://creativecommons.org/ns#" xmlns:dct="http://purl.org/dc/terms/" about="http://subtlepatterns.com" class="notice">Background images from <span property="dct:title">Subtle Patterns</span> (<a rel="cc:attributionURL" property="cc:attributionName" href="http://subtlepatterns.com">Subtle Patterns</a>) / <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/">CC BY-SA 3.0</a></div>