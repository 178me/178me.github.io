---
title: C++ note1
date: 2019-06-04 16:47:09
tags: note
categories: C++
---
函数的一些积累

<!--more-->  

常用头文件
---
**#include <iostream> -> 包含头文件:输入输出流**  
详情了解cin请点击[传送门](https://blog.csdn.net/weixin_41042404/article/details/80934191)  


**using namespace std -> std命名空间**  

**#include <vector> -> 包含向量的头文件**

**#include <algorithm> -> 包含排序方法**   
sort() -> 数组升序排序  
reverse() -> 数组逆序排序

**#include <iterator> -> 迭代器**  

**#include <iomanip> -> 设置输出格式**  
```
setw(2)  //设置字符宽度为2个字节  
setiosflags(ios::left)  //设置文字左对齐

```
**#include <string> -> 字符串操作**  

```
#include <string>
string s;      //定义string对象s
s.length()     //返回字符串长度，即字符个数
s.empty()      //判读字符串是否为空串
s.at(i)        //返回字符串的第i个字符
s[i]           //等同于s.at(i)
s.substr(int i,int j)     //获取从i到j的字符串
其他方法
getline(cin\cout,变量)    //输入或输出变量
```
常用函数  
---
> **[memset()](https://blog.csdn.net/qq_22122811/article/details/52738029)** -> 数组初始化函数



