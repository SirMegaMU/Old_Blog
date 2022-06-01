---
layout: post
title: 树莓派简明使用指北
date: 2021-10-03
tags: 杂项
---

### 基础需求

- 一块树莓派
- 一台可以联网的电脑
- Raspberry Pi Imager[从官网上下载]
- 16G以上的TF卡

### 准备工作

打开Raspberry Pi Imager
![img](https://sirmegamu.github.io/images/posts/2021-10-03/01.png)

使用转换头，将TF卡插入电脑中，

在Operating System中选择Erase`直接在电脑中格式化也行`，在Storage中选择你要烧录的TF卡，点击Write，TF卡中的信息就会被清除。

清除原有信息后将TF卡弹出后再次插入电脑，

在Operating System中选择你想要烧录的系统，在Storage中选择你要烧录的TF卡，点击Write，就会开始自动下载并烧录系统`可能会很慢`。

> 也可以事先从各个支持树莓派的操作系统官网中下载映像文件到本地，在Operating System中选择Custom中选择本地文件进行烧录


### 树莓派带屏幕时的简便安装ingdao

准备好屏幕，鼠标和键盘，将TF卡插入树莓派中，树莓派接电，按引导来就行了

### 无屏幕时的安装


#### 无网线
烧录好之后，你的TF卡中会出现两个盘符，其中一个全是LInux下的文件，在Windows系统下看不见，系统可能会提示你是否格式化`千万不！`。

现在使用一个Linux系统的电脑，读取TF卡，在`/boot`下寻找`ssh`和`wpa_supplicant.conf`两个文件。如果没有，就自己新建它们。

在`wpa_supplicant.conf`中写入一下内容：
~~~
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
ssid="英文网络名称"
psk="网络密码"
priority=1
} 
# 别去掉引号！
~~~
之后正常启动树莓派，在网络服务端查看此树莓派的IP，用ssh连接即可

#### 有网线

在`/boot`下寻找`ssh`文件，如果没有，就自己创建一个

启动树莓派，在网络服务端`也可以扫描IP`找到树莓派的IP，使用ssh连接即可