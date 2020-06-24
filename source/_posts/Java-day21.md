---
title: Java-day21
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 35357
date: 2020-06-22 21:02:21
coverImg:
password:
summary:
---
## 1:字符流(掌握)
###	(1)字节流操作中文数据不是特别的方便，所以就出现了转换流。
	   转换流的作用就是把字节流转换字符流来使用。
###	(2)转换流其实是一个字符流
		字符流 = 字节流 + 编码表
###	(3)编码表
####		A:就是由字符和对应的数值组成的一张表
####		B:常见的编码表
			ASCII
			ISO-8859-1
			GB2312
			GBK
			GB18030
			UTF-8
####		C:字符串中的编码问题
			编码
				String -- byte[]
			解码
				byte[] -- String
###	(4)IO流中的编码问题
####		A:OutputStreamWriter
			OutputStreamWriter(OutputStream os):默认编码，GBK
			OutputStreamWriter(OutputStream os,String charsetName):指定编码。
####		B:InputStreamReader
			InputStreamReader(InputStream is):默认编码，GBK
			InputStreamReader(InputStream is,String charsetName):指定编码
####		C:编码问题其实很简单
			编码只要一致即可
###	(5)字符流
####		Reader
			|--InputStreamReader
				|--FileReader
			|--BufferedReader
####		Writer
			|--OutputStreamWriter
				|--FileWriter
			|--BufferedWriter
###	(6)复制文本文件(5种方式)

## 2:IO流小结(掌握)
###	IO流
####		|--字节流
			|--字节输入流
				InputStream
					int read():一次读取一个字节
					int read(byte[] bys):一次读取一个字节数组
				
					|--FileInputStream
					|--BufferedInputStream
			|--字节输出流
				OutputStream
					void write(int by):一次写一个字节
					void write(byte[] bys,int index,int len):一次写一个字节数组的一部分
					
					|--FileOutputStream
					|--BufferedOutputStream
####		|--字符流
			|--字符输入流
				Reader
					int read():一次读取一个字符
					int read(char[] chs):一次读取一个字符数组
					
					|--InputStreamReader
						|--FileReader
					|--BufferedReader
						String readLine():一次读取一个字符串
			|--字符输出流
				Writer
					void write(int ch):一次写一个字符
					void write(char[] chs,int index,int len):一次写一个字符数组的一部分
					
					|--OutputStreamWriter
						|--FileWriter
					|--BufferedWriter
						void newLine():写一个换行符
						
						void write(String line):一次写一个字符串

## 3:案例(理解 练习一遍)
	A:复制文本文件 5种方式(掌握)
	B:复制图片(二进制流数据) 4种方式(掌握)
	C:把集合中的数据存储到文本文件
	D:把文本文件中的数据读取到集合并遍历集合
	E:复制单级文件夹
	F:复制单级文件夹中指定的文件并修改名称
		回顾一下批量修改名称
	G:复制多级文件夹
	H:键盘录入学生信息按照总分从高到低存储到文本文件
	I:把某个文件中的字符串排序后输出到另一个文本文件中
	J:用Reader模拟BufferedReader的特有功能
	K:模拟LineNumberReader的特有功能