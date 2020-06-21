---
title: Java-day20
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
date: 2020-06-21 20:46:49
author: xing xiao
coverImg:
password:
summary:
tags: Java
categories: 编程
---
## 1:递归(理解)  

###	(1)方法定义中调用方法本身的现象
		举例：老和尚给小和尚讲故事，我们学编程
###	(2)递归的注意事项；
####		A:要有出口，否则就是死递归
####		B:次数不能过多，否则内存溢出
####		C:构造方法不能递归使用
###	(3)递归的案例：
####		A:递归求阶乘
####		B:兔子问题
####		C:递归输出指定目录下所有指定后缀名的文件绝对路径
####		D:递归删除带内容的目录(小心使用)

## 2:IO流(掌握)
###	(1)IO用于在设备间进行数据传输的操作	
###	(2)分类：
####		A:流向
			输入流	读取数据
			输出流	写出数据
####		B:数据类型
			字节流	
					字节输入流
					字节输出流
			字符流
					字符输入流
					字符输出流
####		注意：
			a:如果我们没有明确说明按照什么分，默认按照数据类型分。
			b:除非文件用windows自带的记事本打开我们能够读懂，才采用字符流，否则建议使用字节流。
###	(3)FileOutputStream写出数据
####		A:操作步骤
			a:创建字节输出流对象
			b:调用write()方法
			c:释放资源
			
####		B:代码体现：
			FileOutputStream fos = new FileOutputStream("fos.txt");
			
			fos.write("hello".getBytes());
			
			fos.close();
			
####		C:要注意的问题?
			a:创建字节输出流对象做了几件事情?
			b:为什么要close()?
			c:如何实现数据的换行?
			d:如何实现数据的追加写入?
###	(4)FileInputStream读取数据
####		A:操作步骤
			a:创建字节输入流对象
			b:调用read()方法
			c:释放资源
			
####		B:代码体现：
			FileInputStream fis = new FileInputStream("fos.txt");
			
			//方式1
			int by = 0;
			while((by=fis.read())!=-1) {
				System.out.print((char)by);
			}
			
			//方式2
			byte[] bys = new byte[1024];
			int len = 0;
			while((len=fis.read(bys))!=-1) {
				System.out.print(new String(bys,0,len));
			}
			
			fis.close();
###	(5)案例：2种实现
####		A:复制文本文件
####		B:复制图片
####		C:复制视频
###	(6)字节缓冲区流
####		A:BufferedOutputStream
####		B:BufferedInputStream
###	(7)案例：4种实现
####		A:复制文本文件
####		B:复制图片
####		C:复制视频
		
## 3:自学字符流
###	IO流分类
####		字节流：
			InputStream
				FileInputStream
				BufferedInputStream
			OutputStream
				FileOutputStream
				BufferedOutputStream
		
####		字符流：
			Reader
				FileReader
				BufferedReader
			Writer
				FileWriter
				BufferedWriter