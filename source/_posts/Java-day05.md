---
title: Java-day05
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 10525
date: 2020-06-04 22:54:53
img: https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg
coverImg:
password:
summary:
---
## 1:方法(掌握)  

###	(1)方法：就是完成特定功能的代码块。
		注意：在很多语言里面有函数的定义，而在Java中，函数被称为方法。
###	(2)格式：
		修饰符 返回值类型 方法名(参数类型 参数名1,参数类型 参数名2...) {
			方法体语句;
			return 返回值;
		}

		修饰符：目前就用 public static。后面再详细讲解其他修饰符
		返回值类型：就是功能结果的数据类型
		方法名：就是起了一个名字，方便我们调用该方法。
		参数类型：就是参数的数据类型
		参数名：就是变量
		参数分类：
			实参：实际参与运算的数据
			形参：方法上定义的，用于接收实际参数的变量
		方法体语句：就是完成功能的代码块
		return：结束方法
		返回值：就是功能的结果，由return带给调用者。
###	(3)两个明确：
		返回值类型：结果的数据类型
		参数列表：参数的个数及对应的数据类型
###	(4)方法调用
		A:有明确返回值的方法
			a:单独调用，没有意义
			b:输出调用，不是很好，因为我可能需要不结果进行进一步的操作。但是讲课一般我就用了。
			c:赋值调用，推荐方案
		B:void类型修饰的方法
			a:单独调用
###	(5)案例：
		A:求和方案
		B:获取两个数中的较大值
		C:比较两个数据是否相同
		D:获取三个数中的最大值
		E:输出m行n列的星形
		F:输出nn乘法表
###	(6)方法的注意事项
		A:方法不调用不执行
		B:方法之间是平级关系，不能嵌套定义
		C:方法定义的时候，参数是用，隔开的
		D:方法在调用的时候，不用在传递数据类型
		E:如果方法有明确的返回值类型，就必须有return语句返回。
###	(7)方法重载
		在同一个类中，方法名相同，参数列表不同。与返回值无关。
		
		参数列表不同：
			参数的个数不同。
			参数的对应的数据类型不同。
###	(8)方法重载案例
		不同的类型的多个同名方法的比较。
		
## 2:数组(掌握)  

###	(1)数组：  
	存储同一种数据类型的多个元素的容器。
###	(2)特点：  
	每一个元素都有编号，从0开始，最大编号是长度-1。
	         编号的专业叫法：索引
###	(3)定义格式
		A:数据类型[] 数组名;
		B:数据类型 数组名[];
		
		推荐是用A方式，B方法就忘了吧。
		但是要能看懂
###	(4)数组的初始化
		A:动态初始化
			只给长度，系统给出默认值
			
			举例：int[] arr = new int[3];
		B:静态初始化
			给出值，系统决定长度
			
			举例：int[] arr = new int[]{1,2,3};
			简化版：int[] arr = {1,2,3};
###	(5)Java的内存分配
		A:栈 存储局部变量
		B:堆 存储所有new出来的
		C:方法区(面向对象部分详细讲解)
		D:本地方法区(系统相关)
		E:寄存器(CPU使用)
		
		注意：
			a:局部变量 在方法定义中或者方法声明上定义的变量。
			b:栈内存和堆内存的区别
				栈：数据使用完毕，就消失。
				堆：每一个new出来的东西都有地址
				    每一个变量都有默认值
						byte,short,int,long 0
						float,double 0.0
						char '\u0000'
						boolean false
						引用类型 null
				    数据使用完毕后，在垃圾回收器空闲的时候回收。
###	(6)数组内存图
		A:一个数组
		B:二个数组
		C:三个数组(两个栈变量指向同一个堆内存)
###	(7)数组的常见操作
		A:遍历
			方式1：
				public static void printArray(int[] arr) {
					for(int x=0; x<arr.length; x++) {
						System.out.println(arr[x]);
					}
				}
				
			方式2：
				public static void printArray(int[] arr) {
					System.out.print("[");
					for(int x=0; x<arr.length; x++) {
						if(x == arr.length-1) {
							System.out.println(arr[x]+"]");
						}else {
							System.out.println(arr[x]+", ");
						}
					}
				}
		B:最值
			最大值：
				public static int getMax(int[] arr) {
					int max = arr[0];
					
					for(int x=1; x<arr.length; x++) {
						if(arr[x] > max) {
							max = arr[x];
						}
					}
					
					return max;
				}
				
			最小值：
				public static int getMin(int[] arr) {
					int min = arr[0];
					
					for(int x=1; x<arr.length; x++) {
						if(arr[x] < min) {
							min = arr[x];
						}
					}
					
					return min;
				}
		C:逆序
			方式1：
				public static void reverse(int[] arr) {
					for(int x=0; x<arr.length/2; x++) {
						int temp = arr[x];
						arr[x] = arr[arr.length-1-x];
						arr[arr.length-1-x] = temp;
					}
				}
				
			方式2：
				public static void reverse(int[] arr) {
					for(int start=0,end=arr.length-1; start<=end; start++,end--) {
						int temp = arr[start];
						arr[start] = arr[end];
						arr[end] = temp;
					}
				}
		D:查表
				public static String getString(String[] strArray,int index) {
					return strArray[index];
				}
		E:基本查找
			方式1：
				public static int getIndex(int[] arr,int value) {
					for(int x=0; x<arr.length; x++) {
						if(arr[x] == value) {
							return x;
						}
					}
					
					return -1;
				}
				
			方式2：
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