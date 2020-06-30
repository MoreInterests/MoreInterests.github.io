---
title: Java-踩雷
img: 
top: false
cover: false
toc: true
mathjax: false
date: 2020-06-29 20:20:19
author: xing xiao
coverImg:
password:
summary:
tags: Java
categories: 面试
---
##  下面程序执行的结果是？（ C）  
``` 		
        boolean b=true;
		if(b=false)  //雷区
		{
			System.out.println("a");
		}
		else if(b)
		{
			System.out.println(b);	
		}
		else if(!b)
		{
			System.out.println("c");
		}
		else
			System.out.println("d"); 

```
A.	a               
B.true        
C.	c           
D.d

### 注：'b=false'不是逻辑判断，而是把false赋值给b  
  
## 下面程序执行的结果是？（D）


        int x=2,y=3;
        switch(x)
        {
            default:
            y++;
            case 3:
            y++;
            case 4:
            y++;

        }
        System.out.println("y="+y);

A.  3  

B.  4  

C.  5  

D.  6

 ### 注：没有break，顺序执行  
 

