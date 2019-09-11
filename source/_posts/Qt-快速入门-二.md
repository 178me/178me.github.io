---
title: Qt_快速入门(二)
date: 2019-08-03 14:32:06
tags:
categories:
---
本节讲述Qt中的一些窗口控件如何使用代码创建

<!--more-->

# 菜单栏  

头文件： `#include <QMenuBar>`  

创建方法： `QMenuBar * MenuBar = menuBar()`  

这种方法创建的菜单栏需要使用setMenuBar方法设置到窗口中,菜单栏只能有一个  

# 状态栏  

头文件：`#include <QStatusBar>`  

创建方法： `QStatusBar * status = new QStatusBar(this)`  

状态栏也只能

# 工具栏  

头文件： `#include <QToolBar>`  

创建方法： `QToolBar * toolbar = new QToolBar(this)`  

# 标签  

头文件： `#include <QLabel>`  

创建方法： ` QLabel * label = new QLabel(this)`  

# 按钮  

头文件: `#include <QPushButton>`  

创建方法: `QPushButton * btn = new QPushButton("test",this)`  

按钮要使用new的方式创建在堆区中，否则就会一闪而过。这里使用了两个参数构造函数，第一个是按钮
的名称，第二个是要依赖的窗口，因为代码是在Qwidget类中写的，所以直接使用this。

# 浮动窗口  

头文件：`#include <QDockWidget>`  

创建方法： `QDockWidget * dock = new QDockWidget("浮动窗口",this)`  

# 文本编辑器  

头文件： `#include <QTextEdit>`  

创建方法： `QTextEdit * edit = new QTextEdit(this)`  


