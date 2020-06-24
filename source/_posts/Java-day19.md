---
title: Java-day19
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 48156
date: 2020-06-20 12:36:56
coverImg:
password:
summary:
---
## 1:异常(理解)  

###	(1)程序出现的不正常的情况。
###	(2)异常的体系
		Throwable
			|--Error	严重问题，我们不处理。
			|--Exception
				|--RuntimeException	运行期异常，我们需要修正代码
				|--非RuntimeException 编译期异常，必须处理的，否则程序编译不通过
###	(3)异常的处理：
####		A:JVM的默认处理
			把异常的名称,原因,位置等信息输出在控制台，但是呢程序不能继续执行了。
####		B:自己处理
			a:try...catch...finally
				自己编写处理代码,后面的程序可以继续执行
			b:throws
				把自己处理不了的，在方法上声明，告诉调用者，这里有问题
###	(4)面试题
####		A:编译期异常和运行期异常的区别?
			编译期异常 必须要处理的，否则编译不通过
			运行期异常 可以不处理，也可以处理
####		B:throw和throws是的区别
			throw:
				在方法体中,后面跟的是异常对象名,并且只能是一个
				throw抛出的是一个异常对象，说明这里肯定有一个异常产生了
			throws:
				在方法声明上,后面跟的是异常的类名,可以是多个
				throws是声明方法有异常，是一种可能性，这个异常并不一定会产生
###	(5)finally关键字及其面试题
####		A:finally用于释放资源，它的代码永远会执行。特殊情况：在执行到finally之前jvm退出了
####		B:面试题
			a:final,finally,finalize的区别?
			b:如果在catch里面有return,请问finally还执行吗?如果执行,在return前还是后
				会，前。
				
				实际上在中间。这个上课我们讲过
####		C:异常处理的变形
			try...catch...finally
			try...catch...
			try...catch...catch...
			try...catch...catch...fianlly
			try...finally
###	(6)自定义异常
		继承自Exception或者RuntimeException,只需要提供无参构造和一个带参构造即可
###	(7)异常的注意实现
		A:父的方法有异常抛出,子的重写方法在抛出异常的时候必须要小于等于父的异常 
		B:父的方法没有异常抛出,子的重写方法不能有异常抛出
		C:父的方法抛出多个异常,子的重写方法必须比父少或者小

## 2:File(掌握)
###	(1)IO流操作中大部分都是对文件的操作，所以Java就提供了File类供我们来操作文件
###	(2)构造方法
		A:File file = new File("e:\\demo\\a.txt");
		B:File file = new File("e:\\demo","a.txt");
		C:File file = new File("e:\\demo");
		  File file2 = new File(file,"a.txt");
###	(3)File类的功能(自己补齐)
####		A:创建功能
        public boolean createNewFile():创建文件 如果存在这样的文件，就不创建了
        public boolean mkdir():创建文件夹 如果存在这样的文件夹，就不创建了
        public boolean mkdirs():创建文件夹,如果父文件夹不存在，会帮你创建出来

 * 骑白马的不一定是王子，可能是班长。  

 * 注意：你到底要创建文件还是文件夹，你最清楚，方法不要调错了。
####		B:删除功能
        public boolean delete()
 * 
 * 注意：
 * 		A:如果你创建文件或者文件夹忘了写盘符路径，那么，默认在项目路径下。
 * 		B:Java中的删除不走回收站。
 * 		C:要删除一个文件夹，请注意该文件夹内不能包含文件或者文件夹

####		C:重命名功能
        public boolean renameTo(File dest)
 * 		如果路径名相同，就是改名。
 * 		如果路径名不同，就是改名并剪切。
 * 
 * 路径以盘符开始：绝对路径	c:\\a.txt
 * 路径不以盘符开始：相对路径	a.txt

####		D:判断功能
    public boolean isDirectory():判断是否是目录
    public boolean isFile():判断是否是文件
    public boolean exists():判断是否存在
    public boolean canRead():判断是否可读
    public boolean canWrite():判断是否可写
    public boolean isHidden():判断是否隐藏
####		E:获取功能
    public String[] list():获取指定目录下的所有文件或者文件夹的名称数组
    public File[] listFiles():获取指定目录下的所有文件或者文件夹的File数组

####		F:高级获取功能
####		G:过滤器功能
###	(4)案例：
####		A:输出指定目录下指定后缀名的文件名称
			a:先获取所有的，在遍历的时候判断，再输出
			b:先判断，再获取，最后直接遍历输出即可
####		B:批量修改文件名称