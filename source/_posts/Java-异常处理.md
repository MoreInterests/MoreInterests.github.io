---
title: Java-异常处理
img: 
top: false
cover: false
toc: true
mathjax: false
date: 2020-06-28 11:59:29
author: xing xiao
coverImg:
password:
summary:
tags: Java
categories:
---

#  异常处理 

很多事件并非总是按照人们自己设计意愿顺利发展
的， 而是有能够出现这样那样的异常情况。 例如：
你计划周末郊游， 你的计划会安排满满的， 你计划
可能是这样的： 从家里出发→到达目的→游泳→烧
烤→回家。 但天有不测风云， 当前你准备烧烤时候
天降大雨， 你只能终止郊游提前回家。 “天降大
雨”是一种异常情况， 你的计划应该考虑到这样情
况， 并且应该有处理这种异常的预案。
为增强程序的健壮性， 计算机程序的编写也需要考
虑处理这些异常情况， Java语言提供了异常处理功
能， 本章介绍Java异常处理机制。   
## 从一个问题开始
为了学习Java异常处理机制， 首先看看下面程序。

    //HelloWorld.java文件
    package com.a51work6;
    public class HelloWorld {
        public static void main(String[] args) {
        int a = 0;
        System.out.println(5 / a);
        }
    } 
这个程序没有编译错误， 但会发生如下的运行时错误：

    Exception in thread "main" java.lang.ArithmeticException: / by ze
    at com.a51work6.HelloWorld.main(HelloWorld.java:9)
在数学上除数不能为0， 所以程序运行时表达式（5 / a） 会抛出ArithmeticException异常，ArithmeticException是数学计算异常， 凡是发生数
学计算错误都会抛出该异常。程序运行过程中难免会发生异常， 发生异常并不可
怕， 程序员应该考虑到有可能发生这些异常， 编程
时应该捕获并进行处理异常， 不能让程序发生终
止， 这就是健壮的程序。    

---  
![异常类继承层次](https://cdn.jsdelivr.net/gh/MoreInterests/CDN/P异常类继承层次.jpg)    
  
  
（Java从小白到大牛 509）