---
layout: post
title: 翻墙&Tor-为小白而写
date: 2022-04-16
tags: 资源 
---

# 为何是Tor

Tor是当前最安全的翻墙工具，也是个人认为最适合小白的翻墙工具。免费，易用，安全这三点可以说是已经能满足大部分人的需求。但缺点是网速不稳定且较低，你就别想用这个看高清视频了。不过你既然能获得一个翻墙工具，你就能在互联网上面找到更多的工具，甚至是自己搭建私人的翻墙节点。

### 如何获取Tor

1. 上官网下载<https://www.torproject.org/>，这是最方便的，但对于那些没有翻墙工具的人来说，是上不去它的官网滴

2. 通过邮件获取Tor，向<gettor@torproject.org>发去一封邮件，在主题中描述你的操作系统，和32位或64位客户端的选择

   > Send an email to gettor@torproject.org. In the body of the mail, write the name of your operating system (such  as Windows, macOS, or Linux). GetTor will respond with an email containing links from which you can  download Tor Browser, the cryptographic signature (needed for [verifying the download](https://support.torproject.org/tbb/how-to-verify-signature/)), the fingerprint of the key used to make the signature, and the  package’s checksum. You may be offered a choice of "32-bit" or "64-bit" software: this  depends on the model of the computer you are using; consult  documentation about your computer to find out more.
   
3. 到Github上面的这个[非官方仓库](https://github.com/torproject/tor)下载到源文件，然后自己编译。

### Tor的语言设置

Tor的浏览器其实是基于Firefox制作的，要是使用过Firefox浏览器的话，使用起来肯定会更顺手一些。

Tor默认是使用英文的，你要是不习惯的话可以把游览器显示语言改成中文。当然，你也可以把网页的首选语言改成中文，这样有中文内容的网页会优先给你显示中文翻译。当然，这也会让网页知道你很有可能是中国大陆的网友，也是变相泄露了你的隐私。

![image-20220416205433759](http://megamu.icu/images/posts/2022-04-16/001.png)

### 网桥设置

在设置中的Tor界面就可以设置网桥了，使用Tor的网桥，我们就可以进行翻墙或者是访问暗网。

当然，它这个网桥不是很稳定，当你链接不上时就该换些新网桥

![image-20220416210125809](http://megamu.icu/images/posts/2022-04-16/002.png)

选择从torproject.org获取网桥，填入验证码，稍等待一段时间，就可以获得新网桥了。

