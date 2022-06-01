---
layout: post
title: 安卓x86虚拟机
date: 2022-04-16
tags: 杂项
---

# 起因

前阵子看物联网比赛相关资料的时候看了一下华为的官网，突然一时兴起就想整个鸿蒙玩玩。结果是找了半天都没找到鸿蒙的刷机包，离了刷机包，官网上也没有别的资料，电脑鸿蒙也是找不到官方的映像，只能退而求其次搞个安卓玩玩了。

安卓现在是已经有x86的版本，但是相关的工具还是太少，用起来也不算很方便，但功能是该有的都有了。我就打算先在虚拟机里面装一个玩玩。

### 第一步，虚拟机的创建

先在<https://www.android-x86.org/>下载一个自己想要的系统映像。选择ISO格式的就可以了。之后打开VMware开始新建一个新虚拟机。

![image-20220416130329963](http://megamu.icu/images/posts/2022-04-16/1.png)

兼容性一般选最新的就行了

![image-20220416130506535]http://megamu.icu/images/posts/2022-04-16/2.png)

映像文件选择我们刚刚下载好的安卓x86系统

![image-20220416131137523](http://megamu.icu/images/posts/2022-04-16/3.png)

客户机操作系统选择其他64位或者BSD 64位都可以

![image-20220416131242633](http://megamu.icu/images/posts/2022-04-16/4.png)

选一个存放的位置，下一步

![image-20220416131338157](http://megamu.icu/images/posts/2022-04-16/5.png)

处理器这些自己看这办，够用就行了

![image-20220416131614685](http://megamu.icu/images/posts/2022-04-16/6.png)

虚拟内存同样够用就行，512MB也能跑，但很卡，一般来说4GB就完全够用了

![image-20220416131846362](http://megamu.icu/images/posts/2022-04-16/7.png)

网络先设置不连接，这个后面要用到网络时可以再改，然后下一步

![image-20220416132233841](http://megamu.icu/images/posts/2022-04-16/8.png)

磁盘空间大小看着来，别太小，立即分配这个不选也行，选了在完成设置时就要等一段时间创建磁盘

![image-20220416132345852](http://megamu.icu/images/posts/2022-04-16/9.png)

检查下配置，完成

![image-20220416132417625](http://megamu.icu/images/posts/2022-04-16/10.png)

### 安装系统

选择Installation

![image-20220416133156429](http://megamu.icu/images/posts/2022-04-16/11.png)

选择Create

![image-20220416133437191](http://megamu.icu/images/posts/2022-04-16/12.png)

GPT就不要了，这会影响后面的设置

![image-20220416133629707](http://megamu.icu/images/posts/2022-04-16/13.png)

新建一个分区

![image-20220416133721343](http://megamu.icu/images/posts/2022-04-16/14.png)

选择主分区

![image-20220416133746931](http://megamu.icu/images/posts/2022-04-16/15.png)

空间就全选上吧

![image-20220416133814032](http://megamu.icu/images/posts/2022-04-16/16.png)

设置Bootable，sda1的flags栏会显示boot

![image-20220416134026229](http://megamu.icu/images/posts/2022-04-16/17.png)

之后写入分区信息，确认。完成了就可以选quit退出这个节目里

![image-20220416134114159](http://megamu.icu/images/posts/2022-04-16/18.png)

![image-20220416134151601](http://megamu.icu/images/posts/2022-04-16/19.png)

回到上一个界面，选择我们刚刚建立的sda1

![image-20220416134334343](http://megamu.icu/images/posts/2022-04-16/20.png)

格式化为Linux的ext4格式

![image-20220416134543531](http://megamu.icu/images/posts/2022-04-16/21.png)

选择安装GRUB

![image-20220416134711286](http://megamu.icu/images/posts/2022-04-16/22.png)

选择安装系统目录的读写

![image-20220416134754936](http://megamu.icu/images/posts/2022-04-16/23.png)

之后就会开始在sda1上面安装安卓系统，这需要一段时间。结束了就可以关机了（不是重启！）

### 第三步进入安卓系统

把CD/DVD这里的使用ISO映像文件取消

![image-20220416142058523](http://megamu.icu/images/posts/2022-04-16/24.png)

重启虚拟机。先进入普通模式，如果在普通模式不能正常进入安卓系统，就重启虚拟机，选择debug模式；如果可以正常进入安卓系统，按照安卓系统的引导走就OK了。

![image-20220416142147831](http://megamu.icu/images/posts/2022-04-16/25.png)

![image-20220416142235480](http://megamu.icu/images/posts/2022-04-16/26.png)

输入下面的代码

~~~shell
mount -o remount,rw /mnt
vi /mnt/grub/menu.lst
~~~

在第一个启动项，quite后面加入nomodeset

![image-20220416143049465](http://megamu.icu/images/posts/2022-04-16/27.png)

重新启动，就可以正常进入系统了

### 第四步

进入安卓系统后按照系统的引导走就OK了