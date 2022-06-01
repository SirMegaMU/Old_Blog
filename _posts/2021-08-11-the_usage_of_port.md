---
layout: post
title: 端口基础
date: 2021-08-10
tags: Python
---

## 端口的作用：

设备与外界指定软件/设备通讯的出口  
分配应用程序的信息

端口总数有2^16^个

### 端口的分配

端口分知名端口和动态端口

#### 知名端口（0～1023）

固定使用，不可占用的常用端口

_使用知名端口的程序必须要有root权限_

| 协议名                        | 传输层协议 | 端口号 |
| :---------------------------- | :--------: | ------ |
| ftp数据链接                   | tcp        | 20     |
| ftp控制连接                   | tcp        | 21     |
| **ssh，scp**                  | tcp        | **22** |
| telnet                        | tcp        | 23     |
| **smtp email**                | tcp        | **25** |
| dns服务器与客户端交互         | udp        | 53     |
| dns服务器与辅助域名服务器交互 | tcp        | 53     |
| TFTP                          | udp        | 69     |
| finger                        | tcp        | 79     |
| **http**                      | tcp        | **80** |
| Kerberos Authenticating agent | tcp        | 88     |
| POP3                          | tcp        | 110    |
|ident old identification server system|tcp|113|
|NNTP|tcp|119|
|IMAP3|tcp|220|
|**HTTPS**|tcp|**443**|
|nfs|udp(默认),tcp|2049(默认)|
|vnc|tcp|5901|



#### 动态端口（1024～65535）

不固定分配某种服务，可用于任意软件与任何其他的软件通信的端口数，使用因特网的传输控制协议，或用户传输协议。

### 查看端口

[netstat命令](https://blog.csdn.net/qq_42014600/article/details/90372315) 用于显示各种网络相关信息，如网络连接，路由表，接口状态 (Interface Statistics)，masquerade 连接，多播成员 (Multicast Memberships) 等等。

|参数|作用|
| :-------------------: | :--------- |
|-a| (all)显示所有选项，默认不显示LISTEN相关|
|-t |(tcp)仅显示tcp相关选项|
|-u |(udp)仅显示udp相关选项|
|-n |拒绝显示别名，能显示数字的全部转化成数字。|
|-l |仅列出有在 Listen (监听) 的服務状态|
|-p |显示建立相关链接的程序名|
|-r |显示路由信息，路由表|
|-e |显示扩展信息，例如uid等|
|-s |按各个协议进行统计|
|-c |每隔一个固定时间，执行该netstat命令。|

<script data-ad-client="ca-pub-3585063968143785" async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>