---
title: Java-day01
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 59932
date: 2020-05-31 19:32:11
img: https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg
coverImg:
password:
summary:
---
1:计算机概述(了解)  

	(1)计算机
	(2)计算机硬件
	(3)计算机软件
		系统软件：window,linux,mac
		应用软件：qq,yy,飞秋
	(4)软件开发(理解)
		软件：是由数据和指令组成的。(计算器)
		开发：就是把软件做出来。
		如何实现软件开发呢?
			就是使用开发工具和计算机语言做出东西来
	(5)语言
		自然语言：人与人交流沟通的
		计算机语言：人与计算机交流沟通的
			C,C++,C#,Java
	(6)人机交换
		图形界面：操作方便只管
		DOS命令：需要记忆一些常见的命令

2:键盘功能键的认识和快捷键(掌握)  

	(1)功能键的认识
		tab
		shift
		ctrl
		alt
		windos
		空格
		上下左右
		回车
		截图
	(2)快捷键
		全选	Ctrl+A
		复制	Ctrl+C
		粘贴	Ctrl+V
		剪切	Ctrl+X
		撤销	Ctrl+Z
		保存	Ctrl+S

3:常见的DOS命令(掌握)  

	(1)常见的如下
		盘符的切换
			d:回车
		目录的进入
			cd javase
			cd javase\day01\code
		目录的回退
			cd..
			cd\
		清屏
			cls
		退出
			exit
	(2)其他的几个(了解)
		创建目录
		删除目录
		创建文件
		删除文件
		显示目录下的内容
		删除带内容的目录

4:Java语言概述(了解)  

	(1)Java语言的发展史
		Java之父
		
		JDK1.4.2
		JDK5
		JDK7
	(2)Java语言的特点
		有很多小特点，重点有两个开源，跨平台
	(3)Java语言是跨平台的，请问是如何保证的呢?(理解)
		我们是通过翻译的案例讲解的。
		
		针对不同的操作系统，提高不同的jvm来实现的。
	(4)Java语言的平台
		JavaSE
		JavaME--Android
		JavaEE

5:JDK,JRE,JVM的作用及关系(掌握)  

	(1)作用
		JVM：保证Java语言跨平台
		JRE：Java程序的运行环境
		JDK：Java程序的开发环境
	(2)关系
		JDK：JRE+工具
		JRE：JVM+类库

6:JDK的下载,安装,卸载(掌握)  

	(1)下载到官网。
		A:也可以到百度搜索即可。
		B:我给你。
	(2)安装
		A:绿色版	解压就可以使用
		B:安装版	必须一步一步的安装，一般只要会点击下一步即可
		
		注意：
			建议所有跟开发相关的软件都不要安装在有中文或者空格的目录下。
	(3)卸载
		A:绿色版	直接删除文件夹
		B:安装版	
			a:控制面板 -- 添加删除程序
			b:通过专业的软件卸载工具。(比如360的软件管家卸载)

7:第一个程序：HelloWorld案例(掌握)  

	class HelloWorld {
		public static void main(String[] args) {
			System.out.println("HelloWorld");
		}
	}
	(1)程序解释：
		A:Java程序的最基本单位是类，所以我们要定义一个类。
			格式：class 类名
			举例：class HelloWorld
		B:在类中写内容的时候，用大括号括起来。
		C:Java程序要想执行，必须有main方法。
			格式：public static void main(String[] args)
		D:要指向那些东西呢，也用大括号括起来。
		E:你要做什么呢?今天我们仅仅做了一个简单的输出
			格式：System.out.println("HelloWorld");
			注意：""里面的内容是可以改动的。
	
	(2)Java程序的开发执行流程：
		A:编写java源程序(.java)
		B:通过javac命令编译生成.class文件
		C:通过java命令运行.class文件
	
8:常见的问题(掌握)  

	(1)扩展名被隐藏
		如何找到：工具--文件夹选项--查看--去除隐藏扩展名的那个勾勾
	(2)我要求文件名称和类名一致。
		实际上不这样做也是可以的。
		但是，注意：
			javac后面跟的是文件名+扩展名
			java后面跟的类名不带扩展名
	(3)Java语言严格区分大小写，请注意。
		 还有就是单词不要写错了。
	(4)见到非法字符: \65307肯定是中文问题。
		我们写程序要求标点符号必须全部是英文状态。
	(5)括号的配对问题。
		一般来说，括号都是成对出现的。
	(6)遇到
		在类 HelloWorld 中找不到主方法, 请将主方法定义为
		肯定是主方法的格式问题。

9:path环境变量(掌握)  

	(1)path环境变量的作用
		保证javac命令可以在任意目录下运行。
		同理可以配置qq等
	(2)path配置的两种方案：
		A:方案1(了解)
		B:方案2
			找到环境变量的位置，在系统变量里面
			新建：
				变量名：JAVA_HOME
				变量值：D:\develop\Java\jdk1.7.0_60
			修改：
				变量名：Path
				变量值：%JAVA_HOME%\bin;以前的内容

10:classpath环境变量(理解)  

	(1)classpath环境变量的作用
		保证class文件可以在任意目录下运行
	(2)classpath环境变量的配置
		找到环境变量的位置，在系统变量里面
		新建：
			变量名：classpath
			变量值：E:\JavaSE\day01\code\HelloWorld案例