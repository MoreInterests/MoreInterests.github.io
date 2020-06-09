---
title: Java-day08
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 60636
date: 2020-06-08 18:35:25
img:
coverImg:
password:
summary:
---
1:如何制作帮助文档(了解)  

	(1)写一个类
	(2)加入文档注释
	(3)通过javadoc工具生成即可
		javadoc -d 目录 -author -version ArrayTool.java

2:通过JDK提供的API学习了Math类(掌握)  

	(1)API(Application Programming Interface)
		应用程序编程接口(帮助文档)
	(2)如何使用呢?
		请参照
			day08\code\02_如何使用JDK提供的帮助文档\如何使用帮助文档.txt
	(3)Math类
		A:是针对数学进行操作的类
		B:没有构造方法，因为它的成员都是静态的
		C:产生随机数
			public static double random(): [0.0,1.0)
		D:如何产生一个1-100之间的随机数
			int number = (int)(Math.random()*100)+1;
		E:猜数字小游戏

3:代码块(理解)  

	(1)用{}括起来的代码。
	(2)分类：
		A:局部代码块
			用于限定变量的生命周期，及早释放，提高内存利用率。
		B:构造代码块
			把多个构造方法中相同的代码可以放到这里，每个构造方法执行前，首先执行构造代码块。
		C:静态代码块
			对类的数据进行初始化，仅仅只执行一次。
	(3)静态代码块,构造代码块,构造方法的顺序问题?
		静态代码块 > 构造代码块 > 构造方法
	
4:继承(掌握)  

	(1)把多个类中相同的成员给提取出来定义到一个独立的类中。然后让这多个类和该独立的类产生一个关系，
	   这多个类就具备了这些内容。这个关系叫继承。
	(2)Java中如何表示继承呢?格式是什么呢?
		A:用关键字extends表示
		B:格式：
			class 子类名 extends 父类名 {}
	(3)继承的好处：
		A:提高了代码的复用性
		B:提高了代码的维护性
		C:让类与类产生了一个关系，是多态的前提
	(4)继承的弊端：
		A:让类的耦合性增强。这样某个类的改变，就会影响其他和该类相关的类。
			原则：低耦合，高内聚。
			耦合：类与类的关系
			内聚：自己完成某件事情的能力
		B:打破了封装性
	(5)Java中继承的特点
		A:Java中类只支持单继承
		B:Java中可以多层(重)继承(继承体系)
	(6)继承的注意事项：
		A:子类不能继承父类的私有成员
		B:子类不能继承父类的构造方法，但是可以通过super去访问
		C:不要为了部分功能而去继承
	(7)什么时候使用继承呢?
		A:继承体现的是：is a的关系。
		B:采用假设法
	(8)Java继承中的成员关系
		A:成员变量
			a:子类的成员变量名称和父类中的成员变量名称不一样，这个太简单
			b:子类的成员变量名称和父类中的成员变量名称一样，这个怎么访问呢?
				子类的方法访问变量的查找顺序：
					在子类方法的局部范围找，有就使用。
					在子类的成员范围找，有就使用。
					在父类的成员范围找，有就使用。
					找不到，就报错。
		B:构造方法
			a:子类的构造方法默认会去访问父类的无参构造方法
				是为了子类访问父类数据的初始化
			b:父类中如果没有无参构造方法，怎么办?
				子类通过super去明确调用带参构造
				子类通过this调用本身的其他构造，但是一定会有一个去访问了父类的构造
				让父类提供无参构造
		C:成员方法
			a:子类的成员方法和父类中的成员方法名称不一样，这个太简单
			b:子类的成员方法和父类中的成员方法名称一样，这个怎么访问呢?
				通过子类对象访问一个方法的查找顺序：
					在子类中找，有就使用
					在父类中找，有就使用
					找不到，就报错
	(9)两个面试题：
		A:Override和Overload的区别?Overload是否可以改变返回值类型?
		B:this和super的区别和各自的作用?
	(10)数据初始化的面试题
		A:一个类的初始化过程
		B:子父类的构造执行过程
		C:分层初始化
	(11)案例：
		A:学生和老师案例
			继承前
			继承后
		B:猫狗案例的分析和实现
		
1:代码块是什么?代码块的分类和各自特点?  

用{}括起来的代码。	
分类：
A：局部代码块：用于限定变量的生命周期，及早释放，提高内存利用率
B：构造代码块：把多个构造方法中相同的代码可以放到这里，每个构造方法执行前，首先执行构造代码块。
C：静态大妈快：对类的数据进行初始化，仅仅只执行一次。
静态代码块>构造代码块>局部代码块

2:静态代码块,构造代码块,构造方法的执行流程?    

3:继承概述  

把多个类中相同的成员给提取出来定义到一个独立的类中。然后让这多个类和该独立的类产生一个关系，这多个类就具备了这些内容，这个关系叫继承。

4:继承的好处  

A：提高了代码的复用性
B：提高了代码的维护性
C：让类与类产生了一个关系，是多态的前提

5:Java中继承的特点  

A：Java中类只支持单继承
B：Java中可以多层继承

6:Java中继承的注意事项?以及我们什么时候使用继承?  

A：子类不能继承父类的私有成员
B：子类不能继承父类的构造方法，但是可以通过super去访问
C：不要为了部分功能而去继承

A：继承体现的是： is a的关系
B：采用假设法

7:继承中的成员访问特点  

	A:成员变量
		在子类方法中访问一个变量
	B:成员方法
		在测试类中通过子类对象去访问一个方法

8:继承中构造方法的执行流程?假如父类没有无参构造方法，子类应该怎么办?  

A：子类的构造方法默认会去访问父类的无参构造方法，是为了子类访问父类数据的初始化
B：            子类通过super去明确调用带参构造
	子类通过this调用本身的其他构造，但是一定会有一个去访问了父类的构造
	让父类提供无参构造
9:面试题：  

	方法重写和方法重载的区别?方法重载能改变返回值类型吗?
	Overload （方法重载）同一个类中，出现的方法名相同，参数列表不同的现象
	Override	（方法重写）在子类中，出现和父类中一摸一样的方法声明的现象

	方法重载能改变返回值类型，因为它和返回值类型无关

	this关键字和super关键字分别代表什么?以及他们各自的使用场景和作用。
		this：代表当前类的对象引用
		super：代表父类存储空间的标识。（可以理解为父类的引用，通过这个东西可以访问父类的成员）

10:继承案例练习  

11:猜数字小游戏练习。  

	通过API学习并使用Math类的random()方法。		