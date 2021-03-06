---
title: Linux基本知识
date: 2019-06-05 16:27:11
tags: note 
categories: Linux
---
记录初学Linux所学习的知识
<!--more-->

# 特点  
1. 命令区分`大小写`  
2. 使用`Tab`来补全命令,按两下显示可补全的命令  
3. `上下键`可以查看历史命令  
4. `Ctrl + L`可以清屏  
5. 使用`分号`隔开语句可以实现多条命令  
6. `\`可以断开长命令，增强可读性  
7. 命令后加一个`&`可使命令后台运行  

# Linux文件系统目录结构  

|目录|说明|  
|:-:|:---|  
|/       |根目录  
|/bin    |存放必要的命令的目录  
|/dev    |任何硬件与接口设备以文件的形式放在这个目录下  
|/etc    |存放系统配置文件的目录  
|/home   |系统默认的普通用户家目录 
|/lib    |存放必要运行库的目录  
|/mnt    |各项设备的文件系统挂载点  
|/proc   |存放存储进程和系统信息的目录  
|/root   |系统管理员的家目录  
|/sbin   |存放系统管理员的目录  
|/tmp    |临时文件的存放位置，可供所有用户执行写入操作的特有权限  
|/usr    |UNIX software resource的缩写，是操作系统软件资源所默认放置的目录

- 绝对命令与相对命令  
绝对命令是从`/`开始的，也就是根目录;而相对路径是从当前目录开始  

# Linux基本命令  
大部分的命令可以参考我的[另一篇文章](https://178me.github.io/2019/06/02/shell-note1/#more)，下面补充一些命令：  

1. rmdir  
删除空目录  
rmdir 参数选项 目录名称  

2. ln
为文件创建链接，链接分为硬链接和符号链接两种，默认的链接类型为硬链接
ln 参数选项 源文件或目录 目标文件或目录  
  
|参数|作用|
|:-:|:-:|
|-s|建立符号链接|


3. gzip/gunzip  
压缩/解压缩文件，文件压缩类命令还有bzip2、bunzip2等  
gizp/gunzip 参数选项 文件  
  
|参数|作用|
|:-:|:-:|
|-r|递归压缩|

4. whereis  
寻找命令的可执行文件所在的位置  
whereis 参数 命令名称  

5. ss  
导出socket的统计数据，它显示与netstat命令类似的信息，但能显示比其他工具更详情的TCP状态信息
ss 参数

# 输入/输出重定向和管道命令符的使用

## 输入/输出重定向  

|符号|作用|
|:-:|:-:|
|command < file|将file文件作为command命令的标准输入|
|command > file|将command命令的结果输出到file文件中，若有则覆盖，反之新建|
|command >> file|将command命令的结果输出到file文件中，若有则追加，反之则新建|
|command 2> file|将command命令结果的错误信息输出到file文件中，若有则覆盖，反之新建|
|command &> file|将command命令结果的所有信息输出到file文件中，若有则覆盖，反之新建|

## 管道命令符 

将前一个命令的标准输出作为后一个命令的标准输入  
命令1 | 命令2 




