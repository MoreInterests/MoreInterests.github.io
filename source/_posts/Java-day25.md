---
title: Java-day25
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 18716
date: 2020-06-26 22:25:32
coverImg:
password:
summary:
---
## 1:如何让Netbeans的东西Eclipse能访问。
	在Eclipse中创建项目，把Netbeans项目的src下的东西给拿过来即可。
	注意：修改项目编码为UTF-8
	
## 2:GUI(了解)
###	(1)用户图形界面
		GUI:方便直观
		CLI:需要记忆一下命令，麻烦
###	(2)两个包：
		java.awt:和系统关联较强
		javax.swing:纯Java编写
###	(3)GUI的继承体系
		组件：组件就是对象
			容器组件：是可以存储基本组件和容器组件的组件。
			基本组件：是可以使用的组件，但是必须依赖容器。
###	(4)事件监听机制(理解)
####		A:事件源
####		B:事件
####		C:事件处理
####		D:事件监听
###	(5)适配器模式(理解)
####		A:接口
####		B:抽象适配器类
####		C:实现类
###	(6)案例：
####		A:创建窗体案例
####		B:窗体关闭案例
####		C:窗体添加按钮并对按钮添加事件案例。
			界面中的组件布局。
####		D:把文本框里面的数据转移到文本域
####		E:更改背景色
####		F:设置文本框里面不能输入非数字字符
####		G:一级菜单
####		H:多级菜单
###	(7)Netbeans的概述和使用
####		A:是可以做Java开发的另一个IDE工具。
####		B:使用
			A:四则运算
				a:修改图标
				b:设置皮肤
				c:设置居中
				d:数据校验
####			B:登录注册