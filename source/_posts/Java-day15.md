---
title: Java-day15
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
date: 2020-06-16 19:06:52
author: xing xiao
coverImg:
password:
summary:
tags: Java
categories: 编程
---
## 1:对象数组(掌握)  

###	(1)数组既可以存储基本数据类型，也可以存储引用类型。它存储引用类型的时候的数组就叫对象数组。
###	(2)案例：
		用数组存储5个学生对象，并遍历数组。

## 2:集合(Collection)(掌握)
###	(1)集合的由来?
		我们学习的是Java -- 面向对象 -- 操作很多对象 -- 存储 -- 容器(数组和StringBuffer) -- 数组
		而数组的长度固定，所以不适合做变化的需求，Java就提供了集合供我们使用。
###	(2)集合和数组的区别?
####		A:长度区别
			数组固定
			集合可变
####		B:内容区别
			数组可以是基本类型，也可以是引用类型
			集合只能是引用类型
####		C:元素内容
			数组只能存储同一种类型
			集合可以存储不同类型(其实集合一般存储的也是同一种类型)
###	(3)集合的继承体系结构?
		由于需求不同，Java就提供了不同的集合类。这多个集合类的数据结构不同，但是它们都是要提供存储和遍历功能的，
		我们把它们的共性不断的向上提取，最终就形成了集合的继承体系结构图。
		
		Collection
			|--List
				|--ArrayList
				|--Vector
				|--LinkedList
			|--Set
				|--HashSet
				|--TreeSet
###	(4)Collection的功能概述(自己补齐)
####		A:添加功能
* 		boolean add(Object obj):添加一个元素
* 		boolean addAll(Collection c):添加一个集合的元素
####		B:删除功能
 * 		void clear():移除所有元素
 * 		boolean remove(Object o):移除一个元素
 * 		boolean removeAll(Collection c):移除一个集合的元素(是一个还是所有)
####		C:判断功能
 * 		boolean contains(Object o)：判断集合中是否包含指定的元素
 * 		boolean containsAll(Collection c)：判断集合中是否包含指定的集合元素(是一个还是所有)
 * 		boolean isEmpty()：判断集合是否为空
####		D:获取功能
 * 		Iterator<E> iterator()(重点)
####		E:长度功能
 * 		int size():元素的个数
 * 		面试题：数组有没有length()方法呢?字符串有没有length()方法呢?集合有没有length()方法呢?

####		F:交集(了解)
 * 		boolean retainAll(Collection c):两个集合都有的元素?思考元素去哪了，返回的boolean又是什么意思呢?

####		G:把集合转数组(了解)
 * 		Object[] toArray()

###	(5)Collection集合的遍历
####		A:把集合转数组(了解)
####		B:迭代器(集合专用方式)
###	(6)迭代器
####	A:是集合的获取元素的方式。
####	B:是依赖于集合而存在的。
####		C:迭代器的原理和源码。
			a:为什么定义为了一个接口而不是实现类?
			b:看了看迭代器的内部类实现。
###	(7)Collection集合的案例(遍历方式 迭代器)
		集合的操作步骤：
			A:创建集合对象
			B:创建元素对象
			C:把元素添加到集合
			D:遍历集合
	
####		A:存储字符串并遍历
			import java.util.Collection;
			import java.util.ArrayList;
			import java.util.Iterator;
			
			public class CollectionDemo {
				public static void main(String[] args) {
					//创建集合对象
					Collection c = new ArrayList();
					
					//创建并添加元素
					c.add("hello");
					c.add("world");
					c.add("java");
					
					//遍历集合
					Iterator it = c.iterator();
					while(it.hasNext()) {
						String s =(String) it.next();
						System.out.println(s);
					}
				}
			}
		
####		B:存储自定义对象并遍历
			public class Student {
				private String name;
				private int age;
				
				public Student(){}
				
				public Student(String name,int age) {
					this.name = name;
					this.age = age;
				}
				
				//getXxx()/setXxx()
			}
			
			import java.util.Collection;
			import java.util.ArrayList;
			import java.util.Iterator;
			
			public class StudentDemo {
				public static void main(String[] args) {
					//创建集合对象
					Collection c = new ArrayList();
					
					//创建学生对象
					Student s1 = new Student("林青霞",27);
					Student s2 = new Student("风清扬",30);
					Student s3 = new Student("刘意",30);
					Student s4 = new Student("武鑫",25);
					Student s5 = new Student("刘晓曲",16);
					
					//添加元素
					c.add(s1);
					c.add(s2);
					c.add(s3);
					c.add(s4);
					c.add(s5);
					
					//遍历集合
					Iterator it = c.iterator();
					while(it.hasNext()) {
						Student s = (Student)it.next();
						System.out.println(s.getName()+"---"+s.getAge());
					}
				}
			}

## 3:集合(List)(掌握)  

###	(1)List是Collection的子接口
		特点：有序(存储顺序和取出顺序一致)，可重复。
###	(2)List的特有功能：(自己补齐)
####		A:添加功能
 * 		void add(int index,Object element):在指定位置添加元素

####		B:删除功能
 * 		Object remove(int index)：根据索引删除元素,返回被删除的元素

####	    C:获取功能
 * 		Object get(int index):获取指定位置的元素

####		D:迭代器功能
 * 		ListIterator listIterator()：List集合特有的迭代器

####		E:修改功能
 * 		Object set(int index,Object element):根据索引修改元素，返回被修饰的元素

###	(3)List集合的特有遍历功能
####		A:由size()和get()结合。
####		B:代码演示
					//创建集合对象
					List list = new ArrayList();
					
					//创建并添加元素
					list.add("hello");
					list.add("world");
					list.add("java");
					
					//遍历集合
					Iterator it = list.iterator();
					while(it.hasNext()) {
						String s =(String) it.next();
						System.out.println(s);
					}
					System.out.println("----------");
					
					for(int x=0; x<list.size(); x++) {
						String s =(String) list.get(x);
						System.out.println(s);
					}
###	(4)列表迭代器的特有功能；(了解)
		可以逆向遍历，但是要先正向遍历，所以无意义，基本不使用。
###	(5)并发修改异常
####		A:出现的现象
			迭代器遍历集合，集合修改集合元素
####		B:原因
			迭代器是依赖于集合的，而集合的改变迭代器并不知道。
####		C:解决方案
			a:迭代器遍历，迭代器修改(ListIterator)
				元素添加在刚才迭代的位置
			b:集合遍历，集合修改(size()和get())
				元素添加在集合的末尾
###	(6)常见数据结构
####		A:栈 先进后出
####		B:队列 先进先出
####		C:数组 查询快，增删慢
####		D:链表 查询慢，增删快
###	(7)List的子类特点(面试题)
		ArrayList
			底层数据结构是数组，查询快，增删慢。
			线程不安全，效率高。
		Vector
			底层数据结构是数组，查询快，增删慢。
			线程安全，效率低。
		LinkedList
			底层数据结构是链表，查询慢，增删快。
			线程不安全，效率高。
			
		到底使用谁呢?看需求?
		分析：
			要安全吗?
				要：Vector(即使要，也不使用这个，后面再说)
				不要：ArrayList或者LinkedList
					查询多；ArrayList
					增删多：LinkedList
					
		什么都不知道，就用ArrayList。
###	(8)List集合的案例(遍历方式 迭代器和普通for)
		A:存储字符串并遍历
		B:存储自定义对象并遍历