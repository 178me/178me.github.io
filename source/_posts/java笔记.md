---
title: java笔记
date: 2019-11-30 15:39:27
tags:
categories:
---
初学java的一些知识

<!--more-->
# 第一个程序

- 需要注意一点，java的文件名要与类名相同  
- 使用`javac <源文件>`来编译java源代码,java来运行程序  
- main方法的参数是可以通过运行java的时候传递的，例如java <源程序> 字符串1 字符串n.  
- java源程序运行：java源程序通过编译生成字节码程序，在通过解释器解释执行  

# 源文件声明规则  

- 一个源文件只能有一个public类  
- package语句应该在源文件的首行，package 的作用就是 c++ 的 namespace 的作用，防止名字相同的类产生冲突  
- 如果源文件包含import语句，那么应该放在package语句和类定义之间。如果没有package语句，那么import语句应该在源文件中最前面  

# 数据类型

- byte类型：用在大型数组中节约空间，主要代替整数，因为 byte 变量占用的空间只有 int 类型的四分之一  
- boolean类型：等同C++bool类型
- 其他类型与C++一样








