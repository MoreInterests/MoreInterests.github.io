---
title: Java-day14
top: false
cover: false
toc: true
mathjax: false
author: xing xiao
img: 'https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P05231.jpg'
tags: Java
categories: 编程
abbrlink: 31197
date: 2020-06-14 19:14:08
coverImg:
password:
summary:
---
## 1:正则表达式(理解)  

###	(1)就是符合一定规则的字符串
###	(2)常见规则
####		A:字符
			x 字符 x。举例：'a'表示字符a
			\\ 反斜线字符。
			\n 新行（换行）符 ('\u000A') 
			\r 回车符 ('\u000D')
			
####		B:字符类
			[abc] a、b 或 c（简单类） 
			[^abc] 任何字符，除了 a、b 或 c（否定） 
			[a-zA-Z] a到 z 或 A到 Z，两头的字母包括在内（范围） 
			[0-9] 0到9的字符都包括
			
####		C:预定义字符类
			. 任何字符。我的就是.字符本身，怎么表示呢? \.
			\d 数字：[0-9]
			\w 单词字符：[a-zA-Z_0-9]
				在正则表达式里面组成单词的东西必须有这些东西组成

####		D:边界匹配器
			^ 行的开头 
			$ 行的结尾 
			\b 单词边界
				就是不是单词字符的地方。
				举例：hello world?haha;xixi
			
####		E:Greedy 数量词 
			X? X，一次或一次也没有
			X* X，零次或多次
			X+ X，一次或多次
			X{n} X，恰好 n 次 
			X{n,} X，至少 n 次 
			X{n,m} X，至少 n 次，但是不超过 m 次 
###	(3)常见功能：(分别用的是谁呢?)
####		A:判断功能
			String类的public boolean matches(String regex)
####		B:分割功能
			String类的public String[] split(String regex)
####		C:替换功能
			String类的public String replaceAll(String regex,String replacement)
####		D:获取功能
			Pattern和Matcher
				Pattern p = Pattern.compile("a*b");
				Matcher m = p.matcher("aaaaab");
				
				find():查找存不存在
				group():获取刚才查找过的数据
###	(4)案例
		A:判断电话号码和邮箱
		B:按照不同的规则分割数据
		C:把论坛中的数字替换为*
		D:获取字符串中由3个字符组成的单词
	
## 2:Math(掌握)  

###	(1)针对数学运算进行操作的类
###	(2)常见方法(自己补齐)
####		A:绝对值
		public static int abs(int a)：绝对值	
####		B:向上取整
		public static double ceil(double a):向上取整
####		C:向下取整
		public static double floor(double a):向下取整
####		D:两个数据中的大值
		public static int max(int a,int b):最大值 (min自学)
####		E:a的b次幂
		public static double pow(double a,double b):a的b次幂
####		F:随机数
		public static double random():随机数 [0.0,1.0)
####		G:四舍五入
		public static int round(float a) 四舍五入(参数为double的自学)
####		H:正平方根
		public static double sqrt(double a):正平方根
###	(3)案例：
		A:猜数字小游戏
		B:获取任意范围的随机数
	
## 3:Random(理解)  

###	(1)用于产生随机数的类
###	(2)构造方法:
		A:Random() 默认种子，每次产生的随机数不同
		B:Random(long seed) 指定种子，每次种子相同，随机数就相同
###	(3)成员方法:
		A:int nextInt() 返回int范围内的随机数
		B:int nextInt(int n) 返回[0,n)范围内的随机数

## 4:System(掌握)  

###	(1)系统类,提供了一些有用的字段和方法
###	(2)成员方法(自己补齐)
####		A:运行垃圾回收器
		public static void gc()：运行垃圾回收器。 	
####		B:退出jvm
		public static void exit(int status):终止当前正在运行的 Java 虚拟机。参数用作状态码；根据惯例，非 0 的状态码表示异常终止。
####		C:获取当前时间的毫秒值
		public static long currentTimeMillis():返回以毫秒为单位的当前时间
####		D:数组复制
		public static void arraycopy(Object src,int srcPos,Object dest,int destPos,int length)
 		从指定源数组中复制一个数组，复制从指定的位置开始，到目标数组的指定位置结束。

## 5:BigInteger(理解)  

###	(1)针对大整数的运算
###	(2)构造方法	
		A:BigInteger(String s)
###	(3)成员方法(自己补齐)
		A:加
		B:减
		C:乘
		D:除
		E:商和余数

## 6:BigDecimal(理解)  

###	(1)浮点数据做运算，会丢失精度。所以，针对浮点数据的操作建议采用BigDecimal。(金融相关的项目)
###	(2)构造方法
		A:BigDecimal(String s)
###	(3)成员方法：
####		A:加
		public BigInteger add(BigInteger val):加
####		B:减
		public BigInteger subtract(BigInteger val):减
####		C:乘
		public BigInteger multiply(BigInteger val):乘
####		D:除
		public BigInteger divide(BigInteger val):除
####		E:自己保留小数几位
		public BigInteger[] divideAndRemainder(BigInteger val):返回商和余数的数组

## 7:Date/DateFormat(掌握)  

###	(1)Date是日期类，可以精确到毫秒。
####		A:构造方法
			Date()
			Date(long time)
####		B:成员方法
			getTime()
			setTime(long time)
####		C:日期和毫秒值的相互转换
		案例：你来到这个世界多少天了?
###	(2)DateFormat针对日期进行格式化和针对字符串进行解析的类，但是是抽象类，所以使用其子类SimpleDateFormat
		A:SimpleDateFormat(String pattern) 给定模式
			yyyy-MM-dd HH:mm:ss
		B:日期和字符串的转换
			a:Date -- String
				format()
				
			b:String -- Date
				parse()
		C:案例：
			制作了一个针对日期操作的工具类。
	
## 8:Calendar(掌握)  

###	(1)日历类，封装了所有的日历字段值，通过统一的方法根据传入不同的日历字段可以获取值。
###	(2)如何得到一个日历对象呢?
		Calendar rightNow = Calendar.getInstance();
		本质返回的是子类对象
###	(3)成员方法
		A:根据日历字段得到对应的值
		B:根据日历字段和一个正负数确定是添加还是减去对应日历字段的值
		C:设置日历对象的年月日
###	(4)案例：
		计算任意一年的2月份有多少天?

---
  
看看下面的类，是否都熟悉，简要说明每个类主要是干什么呢?  

	Object类	 Object 是类层次结构的根类。  
	每个类都使用 Object 作为超类。  
	所有对象（包括数组）都实现这个类的方法。 


	Scanner		一个可以使用正则表达式来解析基本类型和字符串的简单文本扫描器。 


	String		String 类代表字符串。Java 程序中的所有字符串字面值（如 "abc" ）都作为此类的实例实现。 


	StringBuffer/StringBuilder		线程安全的可变字符序列。一个类似于 String 的字符串缓冲区，但不能修改。  
	虽然在任意时间点上它都包含某种特定的字符序列，但通过某些方法调用可以改变该序列的长度和内容。
	
	
	Arrays		此类包含用来操作数组（比如排序和搜索）的各种方法。  
	此类还包含一个允许将数组作为列表来查看的静态工厂。 


	Integer		Integer 类在对象中包装了一个基本类型 int 的值。  
	Integer 类型的对象包含一个 int 类型的字段。 


	Character		Character 类在对象中包装一个基本类型 char 的值。  
	Character 类型的对象包含类型为 char 的单个字段。 


	Pattern		正则表达式的编译表示形式。指定为字符串的正则表达式必须首先被编译为此类的实例。  
	然后，可将得到的模式用于创建 Matcher 对象，依照正则表达式，该对象可以与任意字符序列匹配。  
	执行匹配所涉及的所有状态都驻留在匹配器中，所以多个匹配器可以共享同一模式。

	
	Matcher		通过解释 Pattern 对 character sequence 执行匹配操作的引擎。  
	通过调用模式的 matcher 方法从模式创建匹配器。


	Math		Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数。 


	Random		此类的实例用于生成伪随机数流。此类使用 48 位的种子，使用线性同余公式 (linear congruential form) 对其进行了修改（请参阅 Donald Knuth 的The Art of Computer Programming, Volume 3，第 3.2.1 节）。 


	System		System 类包含一些有用的类字段和方法。它不能被实例化。  
	 在 System 类提供的设施中，有标准输入、标准输出和错误输出流；对外部定义的属性和环境变量的访问；  
	 加载文件和库的方法；还有快速复制数组的一部分的实用方法。 

	BigInteger		不可变的任意精度的整数。所有操作中，都以二进制补码形式表示 BigInteger（如 Java 的基本整数类型）。
	
	
	BigDecimal		不可变的、任意精度的有符号十进制数。BigDecimal 由任意精度的整数非标度值 和 32 位的整数标度 (scale) 组成。  
	如果为零或正数，则标度是小数点后的位数。如果为负数，则将该数的非标度值乘以 10 的负 scale 次幂。  
	因此，BigDecimal 表示的数值是 (unscaledValue × 10-scale)。 


	Date		类 Date 表示特定的瞬间，精确到毫秒。 


	DateFormat		DateFormat 是日期/时间格式化子类的抽象类，它以与语言无关的方式格式化并解析日期或时间。  
	日期/时间格式化子类（如 SimpleDateFormat）允许进行格式化（也就是日期 -> 文本）、解析（文本-> 日期）和标准化。  
	将日期表示为 Date 对象，或者表示为从 GMT（格林尼治标准时间）1970 年 1 月 1 日 00:00:00 这一刻开始的毫秒数。
	
	
	Calendar		Calendar 类是一个抽象类，它为特定瞬间与一组诸如 YEAR、MONTH、DAY_OF_MONTH、HOUR 等 日历字段之间的转换提供了一些方法，并为操作日历字段（例如获得下星期的日期）提供了一些方法。  
	瞬间可用毫秒值来表示，它是距历元（即格林威治标准时间 1970 年 1 月 1 日的 00:00:00.000，格里高利历）的偏移量。

