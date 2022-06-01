---
layout: post
title: 解决Ubuntu中的网络视频播放问题
date: 2021-09-29
tags: 杂项
---

### 慕课选的有亿点多，看不过来怎么办?
[优课](http://www.uooc.net.cn/home#/center/course/learn)不容许你在看课程视频时将鼠标移出网站页面，也不能快进拖动视频条，怎么办？

突然灵机一动：可以在电脑中装的Ubuntu**虚拟机**上看一节课的视频，在**物理机**上看另一节课的视频！

两个都开2倍速，这波，这波是超级加倍！

你甚至可以安装多台虚拟机，效率MAX！

### 然而……

Ubuntu本身是没有flash的，我们需要自己给她安装flash插件

### 怎么办？

直接安装flash是无用的我们需要安装flash插件的启动器来为我们的浏览器加装flash插件

~~~ubuntu
sudo apt-get install flashplugin-installer
~~~

