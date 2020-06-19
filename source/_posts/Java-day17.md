---
title: Java-day17
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 30877
date: 2020-06-18 20:20:23
coverImg:
password:
summary:
---
## 1:登录注册案例(理解)

## 2:Set集合(理解)
###	(1)Set集合的特点
		无序,唯一
###	(2)HashSet集合(掌握)
####		A:底层数据结构是哈希表(是一个元素为链表的数组)
####		B:哈希表底层依赖两个方法：hashCode()和equals()
		  执行顺序：
			首先比较哈希值是否相同
				相同：继续执行equals()方法
					返回true：元素重复了，不添加
					返回false：直接把元素添加到集合
				不同：就直接把元素添加到集合
####		C:如何保证元素唯一性的呢?
			由hashCode()和equals()保证的
####		D:开发的时候，代码非常的简单，自动生成即可。
####		E:HashSet存储字符串并遍历
####		F:HashSet存储自定义对象并遍历(对象的成员变量值相同即为同一个元素)
###	(3)TreeSet集合
####		A:底层数据结构是红黑树(是一个自平衡的二叉树)
####		B:保证元素的排序方式
			a:自然排序(元素具备比较性)
				让元素所属的类实现Comparable接口
			b:比较器排序(集合具备比较性)
				让集合构造方法接收Comparator的实现类对象
####		C:把我们讲过的代码看一遍即可
###	(4)案例：
####		A:获取无重复的随机数
####		B:键盘录入学生按照总分从高到底输出
		
## 3:Collection集合总结(掌握)
###	Collection
####		|--List	有序,可重复
			|--ArrayList
				底层数据结构是数组，查询快，增删慢。
				线程不安全，效率高			|--Vector
				底层数据结构是数组，查询快，增删慢。
				线程安全，效率低
			|--LinkedList
				底层数据结构是链表，查询慢，增删快。
				线程不安全，效率高
####		|--Set	无序,唯一
			|--HashSet
				底层数据结构是哈希表。
				如何保证元素唯一性的呢?
					依赖两个方法：hashCode()和equals()
					开发中自动生成这两个方法即可
				|--LinkedHashSet
					底层数据结构是链表和哈希表
					由链表保证元素有序
					由哈希表保证元素唯一
			|--TreeSet
				底层数据结构是红黑树。
				如何保证元素排序的呢?
					自然排序
					比较器排序
				如何保证元素唯一性的呢?
					根据比较的返回值是否是0来决定
					
## 4:针对Collection集合我们到底使用谁呢?(掌握)
	唯一吗?
		是：Set
			排序吗?
				是：TreeSet
				否：HashSet
		如果你知道是Set，但是不知道是哪个Set，就用HashSet。
			
		否：List
			要安全吗?
				是：Vector
				否：ArrayList或者LinkedList
					查询多：ArrayList
					增删多：LinkedList
		如果你知道是List，但是不知道是哪个List，就用ArrayList。
	
	如果你知道是Collection集合，但是不知道使用谁，就用ArrayList。
	
	如果你知道用集合，就用ArrayList。
	
## 5:在集合中常见的数据结构(掌握)
	ArrayXxx:底层数据结构是数组，查询快，增删慢
	LinkedXxx:底层数据结构是链表，查询慢，增删快
	HashXxx:底层数据结构是哈希表。依赖两个方法：hashCode()和equals()
	TreeXxx:底层数据结构是二叉树。两种方式排序：自然排序和比较器排序
		