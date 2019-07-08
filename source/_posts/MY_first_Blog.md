---
title: 我的第一篇博客
date: 2019-05-06 14:46:51
tags:
---

学了点git
<!--more-->

# Git

# **为什么要使用Git**

![GIT功能](MY_first_Blog\功能.png)

- 协同修改

- 数据备份

- 版本管理

- 权限管理

- 历史纪录 

- 分支管理

# Git提交代码五步曲

1. 初始化本地库  
`git init`
2. 设置签名  

```
//系统用户级别
git config --global user.name 名称
git config --global user.email 邮箱  
//项目级别
git config user.name 名称
git config user.email 邮箱 
 
```

3. 添加文件到暂存区
```
git add 文件名      //提交单个文件
git add -A         //提交所有文件
```
4. 提交到本地库  
`git commit -m 描述`
5. 上传到远程仓库  
`git push`

# 对读者的话  
Git是一个很好的代码托管中心，可以把你的代码放到服务器存放，还可以进行版本控制;大家有兴趣可
以去自行找视频学习。






