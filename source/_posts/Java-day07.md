---
title: Java-day07
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
tags: Java
categories: 编程
abbrlink: 59548
date: 2020-06-07 19:48:53
img: https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg
coverImg:
password:
summary:
---
1:成员变量和局部变量的区别(理解)  

	(1)在类中的位置不同
		成员变量：类中方法外
		局部变量：方法定义中或者方法声明上
	(2)在内存中的位置不同
		成员变量：在堆中
		局部变量：在栈中
	(3)生命周期不同
		成员变量：随着对象的创建而存在，随着对象的消失而消失
		局部变量：随着方法的调用而存在，随着方法的调用完毕而消失
	(4)初始化值不同
		成员变量：有默认值
		局部变量：没有默认值，必须定义，赋值，然后才能使用
		
2:类作为形式参数的问题?(理解)  

	(1)如果你看到一个方法需要的参数是一个类名，就应该知道这里实际需要的是一个具体的对象。

3:匿名对象(理解)  

	(1)没有名字的对象
	(2)应用场景
		A:调用方法，仅仅只调用一次的时候。
		b:可以作为实际参数传递。
		
4:封装(理解)  

	(1)隐藏实现细节，提供公共的访问方式
	(2)好处：
		A:隐藏实现细节，提供公共的访问方式
		B:提高代码的复用性
		C:提高代码的安全性
	(3)设计原则
		把不想让外界知道的实现细节给隐藏起来，提供公共的访问方式
	(4)private是封装的一种体现。
		封装：类，方法，private修饰成员变量

5:private关键字(掌握)  

	(1)私有的意义，可以修饰成员变量和成员方法
	(2)特点：
		被private修饰的后的成员只能在本类中被访问
	(3)private的应用：
		以后再写一个类的时候：
			把所有的成员变量给private了
			提供对应的getXxx()/setXxx()方法

6:this关键字(掌握)  

	(1)代表当前类的引用对象
		记住：哪个对象调用方法，该方法内部的this就代表那个对象
	(2)this的应用场景：
		A:解决了局部变量隐藏成员变量的问题
		B:其实this还有其他的应用，明天讲解。

7:构造方法(掌握)  

	(1)作用：用于对对象的数据进行初始化
	(2)格式：
		A:方法名和类名相同
		B:没有返回值类型，连void都不能有
		C:没有返回值
		
		思考题：构造方法中可不可以有return语句呢?
		可以。而是我们写成这个样子就OK了：return;
		其实，在任何的void类型的方法的最后你都可以写上：return;
	(3)构造方法的注意事项
		A:如果我们没写构造方法，系统将提供一个默认的无参构造方法
		B:如果我们给出了构造方法，系统将不再提供默认构造方法
			如果这个时候，我们要使用无参构造方法，就必须自己给出。
			推荐：永远手动自己给出无参构造方法。
	(4)给成员变量赋值的方式
		A:setXxx()
		B:带参构造方法
	(5)标准案例
		class Student {
			private String name;
			private int age;
			
			public Student(){}
			
			public Student(String name,int age) {
				this.name = name;
				this.age = age;
			}
			
			public String getName() {
				return name;
			}
			
			public void setName(String name) {
				this.name = name;
			}
			
			public int getAge() {
				return age;
			}
			
			public void setAge(int age) {
				this.age = age;
			}
		}
		
		测试：
		class StudentDemo {
			public static void main(String[] args) {
				//方式1
				Student s1 = new Student();
				s1.setName("林青霞");
				s1.setAge(27);
				System.out.println(s1.getName()+"---"+s1.getAge());
				
				//方式2
				Student s2 = new Student("刘意",30);
				System.out.println(s2.getName()+"---"+s2.getAge());
			}
		}
		

8:代码：Student s = new Student();做了哪些事情?(理解)  

	(1)把Student.class文件加载到内存
	(2)在栈内存为s开辟空间
	(3)在堆内存为学生对象申请空间
	(4)给学生的成员变量进行默认初始化。null,0
	(5)给学生的成员变量进行显示初始化。林青霞,27
	(6)通过构造方法给成员变量进行初始化。刘意,30
	(7)对象构造完毕，把地址赋值给s变量
		
9:面向对象的练习题(掌握)  

	(1)标准的手机类的定义和测试
	(2)Demo类有求和方法，Test类进行测试。
		什么时候定义成员变量?
		当该变量是用来描述一个类的时候。
	(3)长方形案例
	(4)员工案例
	(5)MyMath案例(自己提供加减乘除并测试)
	
10:static关键字(理解)  

	(1)静态的意思。可以修饰成员变量和成员方法。
	(2)静态的特点：
		A:随着类的加载而加载
		B:优先与对象存在
		C:被类的所有对象共享
			这其实也是我们判断该不该使用静态的依据。
			举例：饮水机和水杯的问题思考
		D:可以通过类名调用
			既可以通过对象名调用，也可以通过类名调用，建议通过类名调用。
	(3)静态的内存图
		静态的内容在方法区的静态区
	(4)静态的注意事项；
		A:在静态方法中没有this对象
		B:静态只能访问静态(代码测试过)
	(5)静态变量和成员变量的区别
		A:所属不同
			静态变量：属于类，类变量
			成员变量：属于对象，对象变量，实例变量
		B:内存位置不同
			静态变量：方法区的静态区
			成员变量：堆内存
		C:生命周期不同
			静态变量：静态变量是随着类的加载而加载，随着类的消失而消失
			成员变量：成员变量是随着对象的创建而存在，随着对象的消失而消失
		D:调用不同
			静态变量：可以通过对象名调用，也可以通过类名调用
			成员变量：只能通过对象名调用
	(6)main方法是静态的
		public:权限最大
		static:不用创建对象调用
		void:返回值给jvm没有意义
		main:就是一个常见的名称。
		String[] args:可以接收数据，提供程序的灵活性
			格式：java MainDemo hello world java
				  java MainDemo 10 20 30