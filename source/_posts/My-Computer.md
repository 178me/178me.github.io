---
title: My_Computer
date: 2019-10-26 23:07:00
tags:
categories:
---
写给没记性又爱折腾的自己

<!--more-->

## 电脑环境
manjaro i3

## 安装步骤  
1. 下载镜像文件
2. 制作启动盘  
3. 完成安装程序

### 安装完之后需要做的事  

1. 配置pacman的软件源  
修改/etc/pacma.conf文件添加源，详情百度  
pacman-mirrors China  //自动设置中国镜像源  

2. 中文字体  
    sudo pacman -S wqy-     //可以安装文泉译所有字体
    将本地语言改为中文，修改/etc/locale.gen，找到zh.CN.China.utf-8,去掉注释，然后locale-gen,如果还不行的话就修改locale.conf文件，具体百度。  

3. 输入法  
    pacman -S fcitx fcitx-qt5 fcitx-sogoupinyin       //这里我使用fcitx的搜狗


4. 浏览器  
    pacman -S google-chrome  
    可以直接使用我配置里的google扩展插件进行离线安装，就可以访问谷歌的一些服务  
    这下我就可以在终端下输入中文字体，也可以欢快的百度了，搞定了这一步就完成了大部分。

5. 现在需要生成一个密钥以便git下载文件  
    - 在家目录下生成一个.ssh文件  
    - 然后使用`ssh-keygen -t rsa -C "你的邮箱"`生成公钥
    - 在git上添加密钥

6. 从github下把我的配置文件下载过来
    - 博客  
        克隆完之后需要下载hexo等工具使用
        1. git config --global user.email "你的邮箱"
        2. git config --global user.name "你的名字"
        3. sudo pacman -S nodejs npm
        4. npm config set registry https://registry.npm.taobao.org
        5. npm install -g hexo-cli
        6. npm install hexo-deployer-git --save  
        在使用hexo d之前检查博客目录下.deployer这个文件，有就删除，不然会报错，然后就可以正常使用了  
    - 配置文件  
        克隆下来放到相对应的位置就可以了，具体看情况  

### 常用软件  
1. 有很多基本的东西你们可以通过[wiki](https://wiki.archlinux.org/index.php/General_recommendations_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) 知道

2. 查找程序,还可以装很多小插件，国产崛起  
yay -S utools

3. 壁纸难以管理，那就用它吧  
sudo pacman -S variety  

4. 好看的虚拟终端加上半透明效果  
sudo pacman -S alacritty compton

5. 你需要一个梯子！
sudo pacman -S electron-ssr  
下载好就从剪贴板导入ssr，开启就好了，export https_proxy=127.0.0.1:12333这个是https的其他的同理，改下端口号就行了

6. 一个好的外国聊天软件，当然也有国内的
sudo pacman -S telegram-desktop  
进入之后设置自定义代理，登录搜索zh就会出来中文包，下载更换即可实现中文。

7. 不嗨歌是没有灵魂的！完美的网易云音乐  
sudo pacman -S netease-cloud-music  
yay -S qcef
顺带提一下，可以修改opt/netease/netease-cloud-music下的netease-cloud-music.bash,在exec上面加上一行内容即可：export XDG_CURRENT_DESKTOP=DDE

### 系统功能设置
1. 触摸板驱动  
查看Archwiki吧，搜索触摸板就可以了

2. 蓝牙  
蓝牙工具可以使用两个工具，blueman和blueberry
两者选一即可，如果单纯相连蓝牙耳机比如我，那就用blueberry吧

3. 笔记本盖上不休屏  
将/etc/systemd/logind.conf中的语句改成`HandleLidSwitch=lock`  

4. 音量调节  
推荐pulseaudio-ctl这个包，man一下就会用了，非常简单  
sudo pamcan -S pulseaudio-ctl  

5. 亮度调节  
一般来说，i3不能直接调亮度，笔记本热键可能也没用，对于intel显卡来说，可以用这个包来调节  
sudo pacman -S xorg-xbacklight  
用法非常简单，使用man xbacklight就可以知道了  
还有一种是在状态栏调节，使用xfce4-power-manager打开电源管理，显示系统托盘就可以使用啦，如果没有的话，那你查查wiki怎么下吧！


### 扩展  
1. man的中文帮助手册  
在arch下一条命令解决  
pacman -S man-pages-zh_cn man-pages-zh_tw
另外其他系统参考[这里](https://www.jianshu.com/p/36b811403a6e)

2. vim中文帮助  
git clone https://github.com/178me/My_Arch.git  
只需要把doc文件夹放进。~/.vim就可以了，其他就可以删除

3. 修改键位  
这里提到一下防止忘记，使用xmodmap命令修改。详情百度  

4. 添加网络模块的支持, 请看 Network Manager.要在 Network manager 里面保存 Wifi 密码，需要安装 GNOME Keyring。

5. 笔记本的一些硬件支持详情 [包括指纹等资料](https://wiki.archlinux.org/index.php/Laptop_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))

6. 修改默认编辑器  
echo export EDITOR=/usr/bin/vim >> ~/.bashrc

7. 修改键盘布局  
setxkbmap us










