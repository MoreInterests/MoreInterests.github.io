---
title: Java-day13
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
tags: Java
categories: 编程
abbrlink: 48028
date: 2020-06-13 23:13:11
coverImg:
password:
summary:
---
## 1:StringBuffer(掌握)  

###	(1)用字符串做拼接，比较耗时并且也耗内存，而这种拼接操作又是比较常见的，为了解决这个问题，Java就提供了
	   一个字符串缓冲区类。StringBuffer供我们使用。
###	(2)StringBuffer的构造方法
		A:StringBuffer()
		B:StringBuffer(int size)
		C:StringBuffer(String str)
###	(3)StringBuffer的常见功能(自己补齐方法的声明和方法的解释)
####		A:添加功能
			public StringBuffer append(String str):可以把任意类型数据添加到字符串缓冲区里面,并返回字符串缓冲区本身

			public StringBuffer insert(int offset,String str):在指定位置把任意类型的数据插入到字符串缓冲区里面,并返回字符串缓冲区本身
####		B:删除功能
			 public StringBuffer deleteCharAt(int index):删除指定位置的字符，并返回本身

 			 public StringBuffer delete(int start,int end):删除从指定位置开始指定位置结束的内容，并返回本身
####		C:替换功能
			public StringBuffer replace(int start,int end,String str):从start开始到end用str替换
####		D:反转功能
			public StringBuffer reverse()
####		E:截取功能(注意这个返回值)
			注意返回值类型不再是StringBuffer本身了

 			 public String substring(int start)

 			 public String substring(int start,int end)

###	(4)StringBuffer的练习(做一遍)
		A:String和StringBuffer相互转换
			String -- StringBuffer
				构造方法
			StringBuffer -- String
				toString()方法
		B:字符串的拼接
		C:把字符串反转
		D:判断一个字符串是否对称
###	(5)面试题
		小细节：
			StringBuffer：同步的，数据安全，效率低。
			StringBuilder：不同步的，数据不安全，效率高。
		A:String,StringBuffer,StringBuilder的区别
		B:StringBuffer和数组的区别?
###	(6)注意的问题：
		String作为形式参数，StringBuffer作为形式参数。
	
## 2:数组高级以及Arrays(掌握)
###	(1)排序
####		A:冒泡排序
			相邻元素两两比较，大的往后放，第一次完毕，最大值出现在了最大索引处。同理，其他的元素就可以排好。
			
			public static void bubbleSort(int[] arr) {
				for(int x=0; x<arr.length-1; x++) {
					for(int y=0; y<arr.length-1-x; y++) {
						if(arr[y] > arr[y+1]) {
							int temp = arr[y];
							arr[y] = arr[y+1];
							arr[y+1] = temp;
						}
					}
				}
			}
			
####		B:选择排序
			把0索引的元素，和索引1以后的元素都进行比较，第一次完毕，最小值出现在了0索引。同理，其他的元素就可以排好。
			
			public static void selectSort(int[] arr) {
				for(int x=0; x<arr.length-1; x++) {
					for(int y=x+1; y<arr.length; y++) {
						if(arr[y] < arr[x]) {
							int temp = arr[x];
							arr[x] = arr[y];
							arr[y] = temp;
						}
					}
				}
			}
###	(2)查找
####		A:基本查找
			针对数组无序的情况
			
			public static int getIndex(int[] arr,int value) {
				int index = -1;
				
				for(int x=0; x<arr.length; x++) {
					if(arr[x] == value) {
						index = x;
						break;
					}
				}
				
				return index;
			}
####		B:二分查找(折半查找)
			针对数组有序的情况(千万不要先排序，在查找)
			
			public static int binarySearch(int[] arr,int value) {
				int min = 0;
				int max = arr.length-1;
				int mid = (min+max)/2;
				
				while(arr[mid] != value) {
					if(arr[mid] > value) {
						max = mid - 1;
					}else if(arr[mid] < value) {
						min = mid + 1;
					}
					
					if(min > max) {
						return -1;
					}
					
					mid = (min+max)/2;
				}
				
				return mid;
			}
###	(3)Arrays工具类
		A:是针对数组进行操作的工具类。包括排序和查找等功能。
		B:要掌握的方法(自己补齐方法)
			把数组转成字符串：
			排序：
			二分查找：
###	(4)Arrays工具类的源码解析
###	(5)把字符串中的字符进行排序
		举例：
			"edacbgf"
			得到结果
			"abcdefg"

## 3:Integer(掌握)
###	(1)为了让基本类型的数据进行更多的操作，Java就为每种基本类型提供了对应的包装类类型
		byte 		Byte
		short		Short
		int			Integer
		long		Long
		float		Float
		double		Double
		char		Character
		boolean		Boolean
###	(2)Integer的构造方法
		A:Integer i = new Integer(100);
		B:Integer i = new Integer("100");
			注意：这里的字符串必须是由数字字符组成
###	(3)String和int的相互转换
		A:String -- int
			Integer.parseInt("100");
		B:int -- String
			String.valueOf(100);
###	(4)其他的功能(了解)
		进制转换
###	(5)JDK5的新特性
		自动装箱	基本类型--引用类型
		自动拆箱	引用类型--基本类型
		
		把下面的这个代码理解即可：
			Integer i = 100;
			i += 200;
###	(6)面试题
		-128到127之间的数据缓冲池问题

## 4:Character(了解)
###	(1)Character构造方法	
		Character ch = new Character('a');
###	(2)要掌握的方法：(自己补齐)
####		A:判断给定的字符是否是大写

		public static boolean isUpperCase(char ch):判断给定的字符是否是大写字符

####		B:判断给定的字符是否是小写

		public static boolean isLowerCase(char ch):判断给定的字符是否是小写字符

####		C:判断给定的字符是否是数字字符

		public static boolean isDigit(char ch):判断给定的字符是否是数字字符

####		D:把给定的字符转成大写

		public static char toUpperCase(char ch):把给定的字符转换为大写字符

####		E:把给定的字符转成小写

		public static char toLowerCase(char ch):把给定的字符转换为小写字符
###	(3)案例：
		统计字符串中大写，小写及数字字符出现的次数