---
title: Java-day10
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
img: https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg
tags: Java
categories: 编程
abbrlink: 47836
date: 2020-06-10 19:41:56
coverImg: 
password:
summary:
---
## 1:形式参数和返回值的问题(理解)  

###	(1)形式参数：
		类名：需要该类的对象
		抽象类名：需要该类的子类对象
		接口名：需要该接口的实现类对象
###	(2)返回值类型：
		类名：返回的是该类的对象
		抽象类名：返回的是该类的子类对象
		接口名：返回的是该接口的实现类的对象
###	(3)链式编程
		对象.方法1().方法2().......方法n();
		
		这种用法：其实在方法1()调用完毕后，应该一个对象；
			      方法2()调用完毕后，应该返回一个对象。
				  方法n()调用完毕后，可能是对象，也可以不是对象。

## 2:包(理解)  

###	(1)其实就是文件夹
###	(2)作用：
		A:区分同名的类
		B:对类进行分类管理
			a:按照功能分
			b:按照模块分
###	(3)包的定义(掌握)
		package 包名;
		
		多级包用.分开。
###	(4)注意事项：(掌握)
		A:package语句必须在文件中的第一条有效语句
		B:在一个java文件中，只能有一个package
		C:如果没有package，默认就是无包名
###	(5)带包的编译和运行
		A:手动式
		B:自动式(掌握)
			javac -d . HelloWorld.java
			
## 3:导包(掌握)  

###	(1)我们多次使用一个带包的类，非常的麻烦，这个时候，Java就提供了一个关键字import。
###	(2)格式：
		import 包名...类名;
		另一种：
			import 包名...*;(不建议)
###	(3)package,import,class的顺序
		package > import > class
	
## 4:权限修饰符(掌握)  

###	(1)权限修饰符
					本类	同一个包下	不同包下的子类	不同包下的无关类
		private		Y
		默认		Y		Y
		protected	Y		Y			Y
		public		Y		Y			Y				Y
###	(2)这四种权限修饰符在任意时刻只能出现一种。
		public class Demo {}		

## 5:常见的修饰符(理解)  

###	(1)分类：
		权限修饰符：private,默认,protected,public
		状态修饰符：static,final
		抽象修饰符：abstract
###	(2)常见的类及其组成的修饰
		类：
			默认,public,final,abstract
			
			常用的：public
		
		成员变量：
			private,默认,protected,public,static,final
			
			常用的：private
			
		构造方法：
			private,默认,protected,public
			
			常用的：public
		
		成员方法：
			private,默认,protected,public,static,final,abstract
			
			常用的：public
###	(3)另外比较常见的：
		public static final int X = 10;
		public static void show() {}
		public final void show() {}
		public abstract void show();

## 6:内部类(理解)  

###	(1)把类定义在另一个类的内部，该类就被称为内部类。
		举例：把类B定义在类A中，类B就被称为内部类。
###	(2)内部类的访问规则
		A:可以直接访问外部类的成员，包括私有
		B:外部类要想访问内部类成员，必须创建对象
###	(3)内部类的分类
		A:成员内部类
		B:局部内部类
###	(4)成员内部类
		A:private 为了数据的安全性
		B:static 为了访问的方便性
		
		成员内部类不是静态的：
			外部类名.内部类名 对象名 = new 外部类名.new 内部类名();
		成员内部类是静态的：
			外部类名.内部类名 对象名 = new 外部类名.内部类名();
###	(5)成员内部类的面试题(填空)
		30,20,10
		
		class Outer {
			public int num = 10;
			
			class Inner {
				public int num = 20;
				
				public viod show() {
					int num  = 30;
					
					System.out.println(num);
					System.out.println(this.num);
					System.out.println(Outer.this.num);
				}
			}
		}
###	(6)局部内部类
		A:局部内部类访问局部变量必须加final修饰。
		B:为什么呢?
			因为局部变量使用完毕就消失，而堆内存的数据并不会立即消失。
			所以，堆内存还是用该变量，而改变量已经没有了。
			为了让该值还存在，就加final修饰。
			通过反编译工具我们看到了，加入final后，堆内存直接存储的是值，而不是变量名。
###	(7)匿名内部类(掌握)
		A:是局部内部类的简化形式
		B:前提
			存在一个类或者接口
		C:格式:
			new 类名或者接口名() {
				重写方法;
			}
		D:本质：
			其实是继承该类或者实现接口的子类匿名对象
###	(8)匿名内部类在开发中的使用
		我们在开发的时候，会看到抽象类，或者接口作为参数。
		而这个时候，我们知道实际需要的是一个子类对象。
		如果该方法仅仅调用一次，我们就可以使用匿名内部类的格式简化。
		
		interface Person {
			public abstract void study();
		}
		
		class PersonDemo {
			public void method(Person p) {
				p.study();
			}
		}
		
		class PersonTest {
			public static void main(String[] args) {
				PersonDemo pd = new PersonDemo();
				pd.method(new Person() {
					public void study() {
						System.out.println("好好学习，天天向上");
					}
				});
			}
		}
		
###	(9)匿名内部类的面试题(补齐代码)
		interface Inter {
			void show();
		}
		
		class Outer {
			//补齐代码
			public static Inter method() {
				return new Inter() {
					public void show() {
						System.out.println("HelloWorld");
					}	
				};
			}
		}
		
		class OuterDemo {
			public static void main(String[] args) {
				Outer.method().show(); //"HelloWorld"
			}
		}


---
1:形式参数和返回值问题   

	形式参数
		基本类型	类名：需要该类的对象
		引用类型	抽象类名：需要改类的子类对象
					接口名：需要该接口的实现类对象
	返回值类型
		基本类型	类名：返回的是该类的对象
		引用类型	抽象类名：返回的是该类的子类对象
					接口名：返回的是该接口的实现类的对象

2:包的定义及注意事项  

	定义：package 报名;
	
	注意事项	A：package语句必须在文件中的定义一条有效语句
				B：在一个Java文件中，只能有一个package
				C：如果没有package，默认就是无包名
	
3:导包及注意事项  

	（1）我们多次使用一个带包的类，非常麻烦，这个时候，Java就提供了一个关键字import
	（2）格式：
				import 包名...类名；
	（3）package ，import，class的顺序
			package>import>class
			
4:四种权限修饰符及其特点  

	(1)权限修饰符
					本类	同一个包下	不同包下的子类	不同包下的无关类
		private		Y
		默认		Y		Y
		protected	Y		Y			Y
		public		Y		Y			Y				Y
	(2)这四种权限修饰符在任意时刻只能出现一种。
		public class Demo {}		
		
5:常见的修饰符及组合  

	(1)分类：
				权限修饰符：private,默认，protected，public
				状态修饰符：static,final
				抽象修饰符：abstract
	(2)常见的类及其组成的修饰
		类：
			默认,public,final,abstract
			
			常用的：public
		
		成员变量：
			private,默认,protected,public,static,final
			
			常用的：private
			
		构造方法：
			private,默认,protected,public
			
			常用的：public
		
		成员方法：
			private,默认,protected,public,static,final,abstract
			
			常用的：public
	(3)另外比较常见的：
		public static final int X = 10;
		public static void show() {}
		public final void show() {}
		public abstract void show();		
		
6:内部类的概述及访问特点  

	(1)把类定义在另一个类的内部，该类就被称为内部类。
		举例：把类B定义在类A中，类B就被称为内部类。
	(2)内部类的访问规则
		A:可以直接访问外部类的成员，包括私有
		B:外部类要想访问内部类成员，必须创建对象
	
	
7:内部类的分类  

	(1)内部类的分类
		A:成员内部类
		B:局部内部类
	(2)成员内部类
		A:private 为了数据的安全性
		B:static 为了访问的方便性
		
		成员内部类不是静态的：
			外部类名.内部类名 对象名 = new 外部类名.new 内部类名();
		成员内部类是静态的：
			外部类名.内部类名 对象名 = new 外部类名.内部类名();
	(3)成员内部类的面试题(填空)
		30,20,10
		
		class Outer {
			public int num = 10;
			
			class Inner {
				public int num = 20;
				
				public viod show() {
					int num  = 30;
					
					System.out.println(num);
					System.out.println(this.num);
					System.out.println(Outer.this.num);
				}
			}
		}
	(4)局部内部类
		A:局部内部类访问局部变量必须加final修饰。
		B:为什么呢?
			因为局部变量使用完毕就消失，而堆内存的数据并不会立即消失。
			所以，堆内存还是用该变量，而改变量已经没有了。
			为了让该值还存在，就加final修饰。
			通过反编译工具我们看到了，加入final后，堆内存直接存储的是值，而不是变量名。
	(5)匿名内部类(掌握)
		A:是局部内部类的简化形式
		B:前提
			存在一个类或者接口
		C:格式:
			new 类名或者接口名() {
				重写方法;
			}
		D:本质：
			其实是继承该类或者实现接口的子类匿名对象
			
