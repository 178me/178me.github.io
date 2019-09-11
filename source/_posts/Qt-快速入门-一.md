---
title: Qt_快速入门(一)
date: 2019-08-03 12:59:51
tags:
categories:
---
本节讲述qt一些基本知识

<!--more-->

# Qt的简介  

Qt是一个跨平台的C++开发库，主要用来开发图形用户应用程序。

Qt是纯C++开发的，所以建议有C++的基础再来学习。 

Qt的优点非常多，比如说跨平台，接口丰富等等。

Qt的成功案例：Linux KDE桌面就是用Qt开发的。

# Qt开发环境的选择   

个人使用的是Qt creator。

manjaro Linux的下载方法就是一条简单的命令  

`sudo pacman -S qtcreator`  

下载完成之后，可以打开软件修改中文界面（默认是英语）

Tools -> Options -> Environment -> Interface 里的Language 修改成Chinese(china)  

不过我的系统在这里有一个小问题，就是选项中没有中文语言，可以用一条命令解决  

`sudo pacman -S qt5-translations`  

之后就可以正常选择了

# Qt的第一个程序  

新建项目 -> 选择Qt Widgets App... ->
Location: 可以修改项目名称和路径 ->
Kits: 构建套件，在实际开发可以选择，我们直接下一步就行了 ->
Details: 可以选择一些基类和界面文件并设置名称，这里我们选择Qwidget，然后把界面文件勾选掉 -> 汇总: 添加版本控制，点击完成即可。

完成之后会生成一些文件  

pro文件 、main.cpp文件和 你创建的类的头文件和实现文件

.pro文件：这个文件可以说是配置文件，可以添加一些模块  

main.cpp会自动生成一些代码，直接运行就可以弹出一个窗口

```
#include "widget.h"
//包含我们自己新建的类的头文件
#include <QApplication>
//包含一个应用程序类的头文件

int main(int argc, char *argv[])
//main程序入口  argc命令行变量的数量   argv命令行变量的数组
{
    QApplication a(argc, argv);
    //实例化应用程序对象，在Qt中，有且只有一个
    Widget w;
    //实例化一个窗口对象
    w.show(); 
    //调用方法显示窗口
    return a.exec();
    //防止窗口一闪而过，进入消息循环
}
```
