---
title: Java-day12
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
tags: Java
categories: 编程
abbrlink: 31581
date: 2020-06-12 11:56:39
coverImg:
password:
summary:
---
## 1:Scanner的使用(了解)
###	(1)在JDK5以后出现的用于键盘录入数据的类。
###	(2)构造方法：
####		A:讲解了System.in这个东西。
			它其实是标准的输入流,对应于键盘录入
####		B:构造方法
			InputStream is = System.in;
			
			Scanner(InputStream is)
####		C:常用的格式
			Scanner sc = new Scanner(System.in);
###	(3)基本方法格式：
		A:hasNextXxx() 判断是否是某种类型的
		B:nextXxx()	返回某种类型的元素
###	(4)要掌握的两个方法
		A:public int nextInt()
		B:public String nextLine()
###	(5)需要注意的小问题
####		A:同一个Scanner对象，先获取数值，再获取字符串会出现一个小问题。
####		B:解决方案：
			a:重新定义一个Scanner对象
			b:把所有的数据都用字符串获取，然后再进行相应的转换
			
## 2:String类的概述和使用(掌握)
###	(1)多个字符组成的一串数据。
		其实它可以和字符数组进行相互转换。
###	(2)构造方法：
		A:public String()
		B:public String(byte[] bytes)
		C:public String(byte[] bytes,int offset,int length)
		D:public String(char[] value)
		E:public String(char[] value,int offset,int count)
		F:public String(String original)
		下面的这一个虽然不是构造方法，但是结果也是一个字符串对象
		G:String s = "hello";
###	(3)字符串的特点
		A:字符串一旦被赋值，就不能改变。
			注意：这里指的是字符串的内容不能改变，而不是引用不能改变。
		B:字面值作为字符串对象和通过构造方法创建对象的不同
			String s = new String("hello");和String s = "hello"的区别?
###	(4)字符串的面试题(看程序写结果)
####		A:==和equals()
			String s1 = new String("hello");
			String s2 = new String("hello");
			System.out.println(s1 == s2);// false
			System.out.println(s1.equals(s2));// true

			String s3 = new String("hello");
			String s4 = "hello";
			System.out.println(s3 == s4);// false
			System.out.println(s3.equals(s4));// true

			String s5 = "hello";
			String s6 = "hello";
			System.out.println(s5 == s6);// true
			System.out.println(s5.equals(s6));// true
####		B:字符串的拼接
			String s1 = "hello";
			String s2 = "world";
			String s3 = "helloworld";
			System.out.println(s3 == s1 + s2);// false
			System.out.println(s3.equals((s1 + s2)));// true

			System.out.println(s3 == "hello" + "world");// false 这个我们错了，应该是true
			System.out.println(s3.equals("hello" + "world"));// true
###	(5)字符串的功能(自己补齐方法中文意思)
####		A:判断功能
			boolean equals(Object obj)
			boolean equalsIgnoreCase(String str)
			boolean contains(String str)
			boolean startsWith(String str)
			boolean endsWith(String str)
			boolean isEmpty()
####		B:获取功能
			int length()
			char charAt(int index)
			int indexOf(int ch)
			int indexOf(String str)
			int indexOf(int ch,int fromIndex)
			int indexOf(String str,int fromIndex)
			String substring(int start)
			String substring(int start,int end)
####		C:转换功能
			byte[] getBytes()
			char[] toCharArray()
			static String valueOf(char[] chs)
			static String valueOf(int i)
			String toLowerCase()
			String toUpperCase()
			String concat(String str)
####		D:其他功能
			a:替换功能 
				String replace(char old,char new)
				String replace(String old,String new)
			b:去空格功能
				String trim()
			c:按字典比较功能
				int compareTo(String str)
				int compareToIgnoreCase(String str) 
###	(6)字符串的案例
		A:模拟用户登录
		B:字符串遍历
		C:统计字符串中大写，小写及数字字符的个数
		D:把字符串的首字母转成大写，其他小写
		E:把int数组拼接成一个指定格式的字符串
		F:字符串反转
		G:统计大串中小串出现的次数