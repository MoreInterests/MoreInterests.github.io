---
title: Java-day24
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 35293
date: 2020-06-25 21:05:49
coverImg:
password:
summary:
---
## 1:多线程(理解)
###	(1)JDK5以后的针对线程的锁定操作和释放操作
		Lock锁
###	(2)死锁问题的描述和代码体现
###	(3)生产者和消费者多线程体现(线程间通信问题)
		以学生作为资源来实现的
		
		资源类：Student
		设置数据类：SetThread(生产者)
		获取数据类：GetThread(消费者)
		测试类：StudentDemo
		
		代码：
			A:最基本的版本，只有一个数据。
			B:改进版本，给出了不同的数据，并加入了同步机制
			C:等待唤醒机制改进该程序，让数据能够实现依次的出现
				wait()
				notify()
				notifyAll() (多生产多消费)
			D:等待唤醒机制的代码优化。把数据及操作都写在了资源类中
###	(4)线程组
###	(5)线程池
###	(6)多线程实现的第三种方案
###	(7)多线程的面试题

## 2:设计模式(理解)
###	(1)面试对象的常见设计原则
		单一
		开闭
		里氏
		依赖注入
		接口
		迪米特
###	(2)设计模式概述和分类
####		A:经验的总结
####		B:三类
			创建型
			结构型
			行为型
###	(3)改进的设计模式
####		A:简单工厂模式
####		B:工厂方法模式
####		C:单例模式(掌握)
			a:饿汉式
			b:懒汉式
###	(4)Runtime
		JDK提供的一个单例模式应用的类。
		还可以调用dos命令。
			