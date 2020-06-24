---
title: Java-day22
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 35677
date: 2020-06-23 16:33:54
coverImg:
password:
summary:
---
## 1:登录注册IO版本案例(掌握)
	要求，对着写一遍。
	
	cn.itcast.pojo User
	cn.itcast.dao UserDao
	cn.itcast.dao.impl UserDaoImpl(实现我不管)
	cn.itcast.game GuessNumber
	cn.itcast.test	UserTest

## 2:数据操作流(操作基本类型数据的流)(理解)
###	(1)可以操作基本类型的数据
333	(2)流对象名称	
		DataInputStream
		DataOutputStream

## 3:内存操作流(理解)
###	(1)有些时候我们操作完毕后，未必需要产生一个文件，就可以使用内存操作流。
###	(2)三种
		A:ByteArrayInputStream,ByteArrayOutputStream
		B:CharArrayReader,CharArrayWriter
		C:StringReader,StringWriter

## 4:打印流(掌握)
###	(1)字节打印流，字符打印流
###	(2)特点：
####		A:只操作目的地,不操作数据源
####		B:可以操作任意类型的数据
####		C:如果启用了自动刷新，在调用println()方法的时候，能够换行并刷新
####		D:可以直接操作文件
			问题：哪些流可以直接操作文件呢?
			看API，如果其构造方法能够同时接收File和String类型的参数，一般都是可以直接操作文件的
###	(3)复制文本文件
		BufferedReader br = new BufferedReader(new FileReader("a.txt"));
		PrintWriter pw = new PrintWriter(new FileWriter("b.txt"),true);
		
		String line = null;
		while((line=br.readLine())!=null) {
			pw.println(line);
		}
		
		pw.close();
		br.close();
			
## 5:标准输入输出流(理解)
###	(1)System类下面有这样的两个字段
		in 标准输入流
		out 标准输出流
###	(2)三种键盘录入方式
####		A:main方法的args接收参数
####		B:System.in通过BufferedReader进行包装
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
####		C:Scanner
			Scanner sc = new Scanner(System.in);
###	(3)输出语句的原理和如何使用字符流输出数据
####		A:原理
			System.out.println("helloworld");
			
			PrintStream ps = System.out;
			ps.println("helloworld");
####		B:把System.out用字符缓冲流包装一下使用
			BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

## 6:随机访问流(理解)
###	(1)可以按照文件指针的位置写数据和读数据。
###	(2)案例：
####		A:写数据
####		B:读数据
####		C:获取和改变文件指针的位置

## 7:合并流(理解)
###	(1)把多个输入流的数据写到一个输出流中。
###	(2)构造方法：
		A:SequenceInputStream(InputStream s1, InputStream s2) 
		B:SequenceInputStream(Enumeration<? extends InputStream> e) 

## 8:序列化流(理解)
###	(1)可以把对象写入文本文件或者在网络中传输
###	(2)如何实现序列化呢?
		让被序列化的对象所属类实现序列化接口。
		该接口是一个标记接口。没有功能需要实现。
###	(3)注意问题：
		把数据写到文件后，在去修改类会产生一个问题。
		如何解决该问题呢?
			在类文件中，给出一个固定的序列化id值。
			而且，这样也可以解决黄色警告线问题
###	(4)面试题：
		什么时候序列化?
		如何实现序列化?
		什么是反序列化?

## 9:Properties(理解)
###	(1)是一个集合类，Hashtable的子类
###	(2)特有功能
		A:public Object setProperty(String key,String value)
		B:public String getProperty(String key)
		C:public Set<String> stringPropertyNames()
###	(3)和IO流结合的方法
		把键值对形式的文本文件内容加载到集合中
		public void load(Reader reader)
		public void load(InputStream inStream)

		把集合中的数据存储到文本文件中
		public void store(Writer writer,String comments)
		public void store(OutputStream out,String comments)
###	(4)案例：
		A:根据给定的文件判断是否有键为"lisi"的，如果有就修改其值为100
		B:写一个程序实现控制猜数字小游戏程序不能玩超过5次

## 10:NIO(了解)
###	(1)JDK4出现的NIO，对以前的IO操作进行了优化，提供了效率。但是大部分我们看到的还是以前的IO
###	(2)JDK7的NIO的使用	
		Path:路径
		Paths:通过静态方法返回一个路径
		Files:提供了常见的功能
			复制文本文件
			把集合中的数据写到文本文件