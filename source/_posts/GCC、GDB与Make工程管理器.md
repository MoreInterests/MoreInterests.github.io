---
title: GCC、GDB与Make工程管理器
img: 
top: false
cover: false
toc: true
mathjax: false
date: 2020-07-18 17:37:43
author: xing xiao
coverImg:
password:
summary:
tags: Makefile
categories: Linux
---
# 一、GNU与GNU工具简介
- GNU的英文全称是"GNU is Not Unix"，又称革奴计划，是由Richard Stallman在1983年9月27日公开发起的。它的目标是创建一套完全自由的操作系统。由于GNU在英文中原意为非洲牛羚，因此GNU计划的图标就是一个牛羚。
- GNU提供各种程序开发工具给编程人员使用。其中包括（但不限于）：
	- 编译工具：将源代码翻译成目标代码的工具。例如GCC、G++等
	- 调试工具：对执行的程序进行断点、单步、单次等调试。例如GDB等
	- 软件管理工具：协助开发人员管理大型程序项目内的源码、资源、文档等工具，例如Make、CVS、Subvision等
	- 其他工具：例如链接生成可执行文件的链接器、文字格式转换的转换工具等。
- 在GNU提供的众多工具内，常用的有GCC、GDB、Make工程管理器这三种。这三种工具也是我们经常使用的在Linux系统内管理C语言程序的工具。
```
/*************一些GNU资源网站*****************/
http://www.gnu.org/
http://gcc.gnu.org/
http://www.kernel.org/
http://www.linux.org/
http://www.linuxdevices.com/
http://sourceforge.net/index.php
/*************一些GNU资源网站end**************/
```
# 二、GCC
## 1、GCC简介
- GCC全程GNU C Compiler，是GNU提供的一款开源免费的C语言编译器，支持编译C、C++、Objective-C、Fortran、Pascal等多种语言。
- GCC可以在多种平台上编译源代码（不过不同平台需要的GCC版本不同），而且GCC具有强大的代码优化能力，其编译效率比其他编译器快20%以上，因此是嵌入式开发领域最受人喜爱的编译器，有些程序开发者甚至称其为“最好用的C语言编译器”。
- GCC主要由分析器、汇编器、链接器、标准C库等组件构成。
## 2、GCC支持的文件格式
- 使用GCC编译器需要特殊的文件名后缀，若文件名无后缀或后缀非法则GCC编译器无法识别。GCC支持的文件类型和后缀常见的有：
	- .c：C语言源代码
	- .cc：C++语言源代码
	- .m：Objective-C语言源代码
	- .i：预处理过的C语言程序
	- .ii：预处理过的C++语言程序
	- .s：汇编语言程序
	- .h：预处理文件（头文件）
	- .o：目标文件
	- .a/.so：编译后的库文件
## 3、GCC编译C语言文件的过程
- GCC将C语言代码编译成最终的可执行程序需要四个步骤：预处理、编译、汇编、链接。
### 1.预处理（Pre-Processing）：
- 主要执行删除程序内注释，加载头文件，替换宏，条件编译等工作
- 需要文件：.c文件
- 生成产物：预处理文件（以.i结尾）
- 使用方法：gcc hello.c -E -o hello.i
### 2.编译（Compiling）：
- 使用编译器进行C语言的语法检查，如果有语法错误，报错，并结束编译过程;如果没有语法错误，把C的源程序转变为汇编代码
- 需要文件：.i文件
- 生成产物：汇编文件（以.s结尾）
- 使用方法：gcc hello.i -S -o hello.s
- 3.汇编（Assembling）：
- 把汇编源文件通过汇编器生成目标文件（二进制机器语言）
- 需要文件：.s文件
- 生成产物：机器码（或称为“目标代码”，以.o结尾）
- 使用方法：gcc hello.s -c -o hello.o
- 4.链接（Linking）：
- 把目标文件执行所依赖的所有二进制的其他目标文件及C的库文件都整合成一个可执行文件的过程
- 需要文件：.o文件及各种动态库或静态库
- 生成产物：可执行程序
- 使用方法：gcc hello.o -o hello	
### 4、代码优化
- 代码优化指的是编译器通过分析代码找出其中不是最优的部分，然后对代码重新组合从而改善程序的执行性能。GCC的代码优化功能十分强大。GCC提供的代码优化有4个等级，分别是：
	- -O0：无优化（默认）
	- -O1：1级优化。使用该选项能减少目标文件大小及执行时间并且不会让编译时间明显增加。在编译较大型的程序时常用。
	- -O2：2级优化。包含1级优化功能并进一步优化生成的目标代码（例如使用更优化的指令调度等），不过会让编译时间增加。
	//2级优化是大多数程序员最常用的代码优化等级，因为它在编译时间与优化长度上取得了一个平衡点。
	- -O3：3级优化。包含2级优化功能并进一步优化生成的目标代码（例如使用特殊的处理器等），不过会让编译时间大幅度增加。
- 虽然代码优化选项可以加快生成的可执行程序的运行速度，不过对于需要调试的代码而言是一个巨大的挑战。因为经过优化的代码与原始代码很可能有诸多不同，使用调试工具时非常有可能跳转到意外的地方从而使调试崩溃。而且，使用越高等级的代码优化，编译时间也会越长。因此代码优化功能要适度使用，也要认清并非所有代码都需要代码优化功能。
- 示例：以下程序在循环部分有明显的不合理运算会拖慢程序的执行速度，分别使用无优化和2级优化编译该代码并查看执行时间的不同
```c
#include<stdio.h>
int main()
{
	double counter;
	double result;
	double temp;
	for(counter = 0; counter < 2000.0*2000.0*2000.0/20.0+2020; counter += (5-1)/4)//注意for()的表达式2和表达式3
	{
		temp = counter / 1979;
		result = counter;
	}   
	printf("Result is %lf\n", result);
	return 0;
}
```
- 关闭优化：gcc test.c -O0 -o test1
- 使用2级优化：gcc test.c -O2 -o test2
- 在执行可执行程序的时候，使用系统的time命令可以查看该程序的运行时间
- time ./test1
- time ./test2
- 可以发现test2的执行时间明显快于test1。

# 三、GDB
## 1、GDB简介
- GDB（GNU symbolic debugger）是GNU的一款代码调试工具，它可以实现查看代码内部结构、打印变量值、设置断点、单步调试等功能。熟练使用GDB工具能够提高我们编程除错的水平。
- 注意：若使用gdb调试代码，则在编译阶段需要添加-g选项。gdb只能调试生成的可执行程序，而不能调试.c源代码文件
- GDB有众多的命令，包含显示代码、设置断点、控制执行、查看栈区、输出变量等功能。
//GDB相关命令参数见附表
## 2、GDB使用流程
- 示例代码：
```c
#include<stdio.h>
int count()
{
	int i;
	int sum=0;
	for(i=1;i<=10;i++)
	{
		sum+=i;
	}
	printf("The sum is %d\n",sum);
	return sum;
}
int main()
{
	count();
	return 0;
}
```

### 1）编译
- 在编译阶段，一定要加上可选项-g（表示开启调试），否则无法使用GDB调试代码
- gcc test.c -g -o test
- 然后就可以启动GDB调试代码了。注意GDB只能调试可执行程序，不能调试C语言源代码文件
- gdb test
### 2）查看GDB调试的文件
- 我们可以使用list命令查看载入的文件。默认情况下list显示10行，可以使用set listsize来设置显示行数
### 3）设置断点
- 我们可以使用break命令设置断点。当程序运行至断点处会停下。设置断点的方式有：
    - break function：在指定函数定义处设置断点
    - break linenum：在指定行处设置断点
### 4）查看断点
- 设置断点后可以使用info breakpoints命令查看断点信息
### 5）运行
- 使用run命令让代码从头运行，当代码运行至断点处时会停下
- 使用continue命令让代码继续运行至下一个断点处
### 6）查看变量值
- 我们可以使用p+变量名来打印变量信息
### 7）恢复运行
- 可以使用finish命令让程序运行完成
- 可以使用clear命令清除所有断点，也可以用clear+断点号清除指定断点

# 四、Make工程管理器
- Make工程管理器是一个用来管理多文件的文件转化管理工具。它可以通过依赖关系将某种文件转化为目标文件target。大多数情况下，Make工程管理器用于调用GCC编译器将源代码编译成目标代码，再将目标代码整合生成可执行程序。使用Make工程管理器的时候一定要掌握两个概念：目标（target）和依赖关系（dependency）。目标就是要生成的文件，依赖关系就是生成目标文件需要的文件。
- Make工程管理器使用名为"makefile"的脚本文件来确定依赖关系并生成目标文件。因此我们必须熟练掌握makefile的写法才能正确使用Make工程管理器。
- Make工程管理器对参与编译的代码的管理原则是“若未改动则不参与”，若makefile发现这次参与编译的某些文件在上次编译后一直未被修改，则本次编译会自动忽略这些文件，从而减少编译时间。
- 也就是说，Make工程管理器是通过文件的时间戳来识别文件是否应该参与编译的。
## 1、makefile基本规则
- 虽然makefile不是一门专门的编程语言，但是我们也需要使用特定的格式来编写makefile文件。
```
示例1：使用makefile输出helloworld
首先使用vim创建一个文本文件，命名为makefile。内容为：
all:
	echo "hello world"
注意：在makefile内，每个命令行前面必须以"Tab键"开头，否则会出现使用错误：missing separator
```
- 在这个简单的makefile中，"all"就是我们的生成目标（target），每个生成目标都需要放在冒号之前。"all:"下面的命令代表生成目标需要的命令，我们也称之为“规则”，在这个示例内我们生成目标只有一个规则，实际上可以有多条规则。在这个简单的makefile中，我们规定了生成的目标为"all"，而生成该目标需要一个echo命令。
- 若我们想运行这个makefile查看运行效果，我们无需像Shell脚本一样给该makefile添加执行权限，而是使用make命令调用Make工程管理器，Make工程管理器会自动按照makefile的内容来执行。
- 使用该makefile：make 或 make all
- 在调用makefile的时候，终端会先输出一遍生成目标的规则，然后输出生成的目标。若我们不想看到输出的规则，则我们可以在规则前面加上'@'：
```
all:
	@echo "hello world"
这样就不会输出规则了。
```	
- 当然，一个makefile不仅仅只能生成一个目标，一个makefile是可以支持生成多个目标的，只不过我们需要调用相应的make命令来告诉Make工程管理器需要生成哪个目标。
```
示例2：在示例1的基础上添加一个新的目标
all:
	@echo "hello world"
test:
	@echo "nihao farsight"
在示例1的基础上添加了一个新的目标"test"，此时我们可以的makefile文件就可以生成两个目标了。
生成目标all：make 或 make all
生成目标test：make test
```
- 我们在运行示例2的makefile时会发现，若我们执行make，则只会输出目标all。这是由makefile的逻辑决定的，在未指定make目标的情况下（即缺省目标的情况下），makefile默认只生成第一个目标。
- 那么能不能在make的时候也生成test目标呢？当然可以，我们可以这样修改makefile：
```
示例3：修改示例2，使得make也可以生成test目标
all:test
	@echo "hello world"
test:
	@echo "nihao farsight"
```
- 在示例3中，我们在"all:"后面添加了一个新的字段"test"，这个字段就是“依赖关系”。"all:test"这个字段的意思就是：生成目标all需要依赖目标test。这样makefile在生成all之前会先去生成目标test，在生成目标test后才会去生成目标all。一个目标可以有多个依赖关系，若一个目标有多个依赖关系，则所有的依赖关系都写在冒号之后，用空格分隔。
- 因此编写一个makefile最重要的就是要弄懂需要生成的目标，以及生成这些目标需要的依赖关系。“目标”与“依赖”是使用makefile的重点，我们需要重点关注。

## 2、使用makefile编译C语言文件
- 有了以上对makefile的基本认识，我们来试图编写一个用于编译C语言文件的makefile。
- 首先需要准备代码，注意头文件hello.h的格式：
```
//文件hello.h
#ifndef __MY_H_INCLUDE__
#define __MY_H_INCLUDE__
#include<stdio.h>

#endif

//文件hello.c
#include"hello.h"
int main()
{
	printf("hello world");
}
```
- 然后编写一个makefile：
```
示例4：编译hello.c的makefile文件
all:hello.h hello.c
	gcc hello.c -o hello
```
- 此时我们运行命令make，就可以编译文件hello.c和hello.h生成文件hello。
- 但是，几个简单的文件使用makefile实在是太浪费了。现在我们准备多个C语言源文件，然后使用makefile对这几个C语言源文件进行编译：
```
//文件my.h
#ifndef __MY_H_INCLUDE__
#define __MY_H_INCLUDE__
#include<stdio.h>
int foo();
int simple();
int hello();

#endif
//文件foo.c
#include"my.h"
int foo()
{
	printf("this is foo\n");
}
//文件simple.c
#include"my.h"
int simple()
{
	printf("this is simple\n");
}
//文件hello.c
#include"my.h"
int hello()
{
	printf("this is hello\n");
}
//文件main.c，主函数所在文件，程序入口
#include"my.h"
int main()
{
	printf("Hello world");
	foo();
	simple();
	hello();//分别调用三个文件内的函数
	return 0;
}
```
- 此时我们再编写一个编译多个文件的makefile：
```
示例5：将多个.c文件编译生成最终的可执行程序
all:main.o foo.o simple.o hello.o
	gcc main.o foo.o simple.o hello.o -o hello
main.o:main.c
	gcc main.c -c -o main.o
foo.o:foo.c
	gcc foo.c -c -o foo.o
simple.o:simple.c
	gcc simple.c -c -o simple.o
hello.o:hello.c
	gcc hello.c -c -o hello.o
clean:
	rm *.o
```	
- 示例5的makefile与常规的管理大型程序的makefile已经十分接近了。这里注意makefile的最后，我们添加了一个clean目标，用于清除生成的.o文件。
- 通过示例5的makefile我们可以看到，在编写makefile的时候，最重要的是需要将目标以及该目标的依赖关系弄清楚。若没有弄清楚目标和依赖关系，则编写的makfile也会有各种问题。
- 若我们已经执行make编译生成了可执行文件hello，此时又修改代码，会有什么现象呢？
    - 例如，我们此时修改main.c而其他.c文件不动：
```
//文件main.c，修改后的main.c
#include"my.h"
int main()
{
	printf("Hello world");
	foo();
	simple();
	hello();//分别调用三个文件内的函数
	hello();//又调用一次hello()函数
	return 0;
}
```
- 修改main.c后再执行make。我们会发现makefile只会针对main.c和main.o重新编译。
- 这是因为makefile为了节省编译时间，只会重新编译被修改过的文件。也就是说，若文件未被修改（时间戳没变）则不会重新编译，若文件被修改（时间戳改变）则重新编译。

## 3、makefile假目标
- 在示例5中我们在makefile最后添加了一个clean目标用于清除生成的.o文件。但是添加了clean目标后会造成一个问题：若我们的C语言源文件内恰好有一个clean.c文件，则我们执行make clean的时候，makefile不会执行清除文件命令，而是会编译clean.c生成clean文件。
- 在实际的程序开发中也难免出现所定义的目标与已存在的文件重名的情况。针对于这种情况，makefile提供了“假目标（phony target）”这个用法。
- 假目标使用.PHONY关键字定义，注意.PHONY关键字都是大写。
```
示例6：给示例5添加假目标
.PHONY:clean
all:main.o foo.o simple.o hello.o
	gcc main.o foo.o simple.o hello.o -o hello
main.o:main.c
	gcc main.c -c -o main.o
foo.o:foo.c
	gcc foo.c -c -o foo.o
simple.o:simple.c
	gcc simple.c -c -o simple.o
hello.o:hello.c
	gcc hello.c -c -o hello.o
clean:
	rm *.o
```
- 采用.PHONY关键字定义clean了之后，make不会将clean作为一个文件处理而是当做一个目标去处理。

## 4、makefile变量
### 1）使用makefile变量
- 只要是程序开发人员对变量肯定都十分熟悉。为了方便程序开发人员使用，makefile内也有变量，其变量的用法类似于Shell编程的变量用法。使用makefile变量可以让makefile变得更加简洁、方便维护。
- makefile的变量定义十分简单，格式为：
	- 变量名 = 变量值
- 其中变量值可以有多个。类似于Shell编程中的变量定义，不过赋值号左右无需考虑空格的问题。
- 若要引用定义过的变量，则可以：
	- $(变量名) 或 ${变量名}
即可。
```
示例7：将示例6内部分字段替换为变量形式：
.PHONY:clean
OBJS = main.o foo.o simple.o hello.o
OBJ = hello
CC = gcc
RM = rm

$(OBJ):$(OBJS) 
	$(CC) $(OBJS) -o $(OBJ)
main.o:main.c
	$(CC) main.c -c -o main.o
foo.o:foo.c
	$(CC) foo.c -c -o foo.o
simple.o:simple.c
	$(CC) simple.c -c -o simple.o
hello.o:hello.c
	$(CC) hello.c -c -o hello.o
clean:
	$(RM) $(OBJS) $(OBJ)
```	
- 在这个makefile中，我们引入了4个变量：
	- OBJS：表示生成最终可执行程序所依赖的目标文件
	- OBJ：表示最终生成的可执行文件名
	- CC：表示编译器使用GCC
	- RM：用于指示删除文件命令
- 采用变量来书写makefile是十分方便的。若我们需要修改makefile的内容，则只需修改变量定义处即可，而无需修改makefile内的内容。
- 需要注意的是，$符号对makefile有特殊含义。若我们想在makefile内使用echo命令打印$符号则需要连续两个$$才可以。
- makefile内预定义了一些变量，这些变量为：
	- AR：库文件维护程序的名称，默认为ar
	- AS：汇编程序的名称，默认为as
	- CC：C编译器的名称，默认为gcc
	- CPP：C预处理器的名称，默认为gcc -E
	- CXX：C++编译器的名称，默认为g++
	- FC：Fortran编译器的名称，默认为f77
	- RM：文件删除命令的名称，默认为rm -f
	- ARFLAGS：库文件选项，无默认值
	- ASFLAGS：汇编程序选项，无默认值
	- CFLAGS：C编译器选项，无默认值
	- CPPFLAGS：C预处理器选项，无默认值
	- CXXFLAGS：C++编译器选项，无默认值
	- FFLAGS：Fortran编译器选项，无默认值

### 2）makefile的自动推断
- 使用变量后确实方便了makefile的编写，但这不是makefile的最终形态。若目标文件OBJS过多，则每次在写规则的时候都会十分麻烦。而且我们发现，使用了变量后，大多数的规则内容都显得重复。若我们可以自动让makefile寻找OBJS内容然后生成目标，则会大大简化makefile的书写工作。
- 这时，我们可以使用makefile提供的自动变量。当我们的编译目标有多个的时候，使用自动变量会大大简化makefile的编写工作。自动变量有：
	- $@：表示一个规则中的目标
	- $^：表示规则的所有依赖的文件名。注意一般情况下$^只会在makefile内出现一次
	- $<：表示规则的第一个依赖的文件名。若为自动推导，则为该规则添加第一个依赖文件名
```
示例8：将示例7使用自动变量改写
.PHONY:clean
OBJS = main.o foo.o simple.o hello.o
OBJ = hello
CC = gcc
RM = rm

$(OBJ):$(OBJS) 
	$(CC) $^ -o $@
main.o:main.c
	$(CC) $< -c -o $@
foo.o:foo.c
	$(CC) $< -c -o $@
simple.o:simple.c
	$(CC) $< -c -o $@
hello.o:hello.c
	$(CC) $< -c -o $@
clean:
	$(RM) $(OBJS) $(OBJ)
```
- makefile的功能很强大，它可以自动推导文件以及文件依赖关系以及后面的命令。例如：
```
main.o:main.c
	$(CC) $< -c -o $@
```
- 当makefile执行该命令的时候，它会首先查看$@的内容，makefile会自动推断出此处$@应是main.o。然后查看$<的内容，makefile会根据指定的依赖关系自动推断出生成main.o需要main.c文件。这样我们所有的规则都可以使用自动变量的形式来书写了。
- 既然所有的规则都已经使用$(CC) $^ -c -o $@改写了，那所有的目标和依赖关系可不可以也被某些写法替代呢？也就是说，能不能将所有的
```
which.c:which.o
	$(CC) $< -c -o $@
```
- 都合并到一起呢？当然可以！
```
示例9：更加简化的makefile，将所有的which.o:which.c都合并
.PHONY:clean
OBJS = main.o foo.o simple.o hello.o
OBJ = hello
SRC = main.c foo.c simple.c hello.c
CC = gcc
RM = rm

$(OBJ):$(OBJS) 
	$(CC) $^ -o $@
%.o:%.c
	$(CC) $< -c -o $@

clean:
	$(RM) $(OBJS) $(OBJ)
```
- 在示例9的makefile内，'%'表示的是makefile的通配符（类似于Shell编程内的*）。示例9的makefile的运行流程如下：
    - 1.makefile要生成$(OBJ)（即hello），需要依赖$(OBJS)（即所有.o文件）。但是此时目录内没有.o文件
    - 2.继续向下，发现%.o:%.c字段，使用通配符匹配，发现此时%.o的%应为main，即%.o=main.o
    - 3.匹配成功，那么后面的%.c自动推断为main.c
    - 4.执行规则$(CC) $< -c -o $@，将main.c填入$<的位置，将main.o填入$@的位置。
    - 5.返回$(OBJ):$(OBJS)处，试图生成hello，发现还缺少其他的.o文件
    - 6.重复步骤2、3、4，直至所有$(OBJS)都被生成
    - 7.返回$(OBJ):$(OBJS)处，生成hello
- 我们的makefile功能更强大了！