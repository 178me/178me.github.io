---
title: pacman
date: 2020-01-02 18:16:35
tags:
categories:
---

记录pacman用法
<!--more-->

# 安装软件

pamcna -S 软件名

还可以使用

pacman -S $()

- fish 不加$符号

# 更新软件源

pacman -Sy

pacman -Syy     //强制刷新

# 更新软件包

pacman -Su

一般直接用 pacman -Syu

# 搜素软件包

pacman -Ss 软件名

# 删除本地缓存包

pacman -Sc

# 卸载软件

pacman -R 软件名

pacman -Rs 软件名       //删除依赖

pacman -Rns 软件名      //完全删除，包括配置等等

# 查询安已装软件

pacman -Qq              //不显示版本号

pamcan -Qdt             //不再被需要的依赖

pacman -Qe              //自己安装的软件

可以使用pacman -Qeq 导出自己的软件名到文件中 然后使用pacman -S $(cat 存放软件名的文件)到自己的新电脑















