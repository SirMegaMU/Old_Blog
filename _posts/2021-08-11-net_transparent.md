---
layout: post
title: 网络传输基础
date: 2021-08-10
tags: Python
---

# 网络传输

网络传输是指用一系列的线路经过电路的调整变化依据网络传输协议来进行通信的过程。

其中网络传输需要介质，也就是网络中发送方与接收方之间的物理通路，它对网络的数据通信具有一定的影响。网络协议即网络中传递、管理信息的一些规范。

网络协议通常被分为几个层次，通信双方只有在共同的层次间才能相互联系。

## 网络传输方式

网络传输根据数据发送方式分类，主要分两种

### 面向有连接型

依赖发送方和接收器之间的显示通信和阻塞以管理双方的数据传输.网络系统需要在两台计算机之间发送数据之前先建立连接的一种特性。
面向连接的协议比面向无连接的协议在可靠性上有着显著的优势，但建立连接前必须等待接收方响应，传输信息过程中必须确认信息是否传到，断开连接时需要发出响应信号等，无形中加大了面向连接协议的资源开销。

| 协议              | 功能 |
| :---------------- | :--- |
| TCP | 面向连接的、可靠的、基于字节流的传输层通信协议，能够动态地适应互联网络的这些特性，而且具备面对各种故障时的健壮性。只能一对一传输。严格区分客户端与服务器。![image-20210810175731914](http://sirmegamu.github.io/images/posts/2021-08-11-net_transparent/net_transparent5.png) |



#### 客户端

客户端向服务器发送连接请求  
客户端向服务器发送/接收信息

![image-20210810192207666](http://sirmegamu.github.io/images/posts/2021-08-11-net_transparent/net_transparent1.png)

~~~python
# 导入模块
import socket

# 创建套接字
tcp_client_socket =socket.socket(socket.AF_INET,socket.SOCK_STREAM)

# 与服务器建立连接
tcp_client_socket.connect(("192.168.0.105",8080))

# 发送数据
tcp_client_socket.send("你好".encode())

# 接收数据
recv_data = tcp_client_socket.recv(1024)
print("来自服务器的消息：")

# 解码
print(recv_data.decode())

# 关闭套接字
tcp_client_socket.close
~~~

#### 服务器

服务器接收请求，并向客户端发送/接受信息。

![image-20210810205401597](http://sirmegamu.github.io/images/posts/2021-08-11-net_transparent/net_transparent8.png)

~~~python
# 导入模块
import socket

# 创建套接字
tcp_server_socket = socket.socket(socket.AF_INET,socket.SOCK_STREAM)

# 绑定IP和端口
tcp_server_socket.bind(("",8082))
while True:
# 开启监听，设置为被动模式(不能主动发信息，阻塞)，设置最大连接数
    tcp_server_socket.listen(128)

    # 等待客户端连接(阻塞)
    new_client_socket, ip_port  = tcp_server_socket.accept() 
    """返回一个新的套接字对象;返回客户端IP地址和端口号元组"""
    print("客户端{}端口{}已连接！".format(ip_port[0],int(ip_port[1])))
    while True:
    # 接收/发送信息
        recv_data = new_client_socket.recv(1024)
        if len(recv_data.decode()) ==0:
            print("客户端已断开！")
            # 关闭套接字
            new_client_socket.close
            break
        else:
            try:
                print("来自{0}用户{1}端口的信息：".format(ip_port[0],str(ip_port[1])),end="   ")
                print(recv_data.decode())
            except:
                print("解码失败")
        new_client_socket.close

# 关闭服务器(不再接收新的连接，已有的可以继续连接)
tcp_server_socket.close
~~~


### 面向无连接型

通信双方不需要事先建立一条通信线路，而是把每个带有目的地址的包（报文分组）送到线路上，由系统自主选定路线进行传输。不管对方是否有响应，是否有回馈，只管将信息发送出去。

IP、UDP协议就是一种无连接协议。

| 协议 | 功能                                                         |
| ---- | ------------------------------------------------------------ |
| IP   | TCP/IP体系中的网际层协议。根据端到端的设计原则，IP只为主机提供一种无连接、不可靠的、尽力而为的数据包传输服务。IP不保证分组的交付时限和可靠性，所传送分组有可能出现丢失、重复、延迟或乱序等问题。 |
| UDP  | Internet 协议集支持一个无连接的传输协议。UDP 为应用程序提供了一种无需建立连接就可以发送封装的 IP 数据包的方法。UDP协议的控制选项较少，在数据传输过程中延迟小、数据传输效率高，适合对可靠性要求不高的应用程序，或者可以保障可靠性的应用程序，可以进行广播。 |



#### 发送信息

![发送信息](http://sirmegamu.github.io/images/posts/2021-08-11-net_transparent/net_transparent1.png)

~~~python
# 导入模块
import socket

# 创建套接字(使用IPv4,UDP)
udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

# 发送套接字
# .sendto(要发送数据的二进制格式，（对方IP地址和端口号）的元组)
udp_socket.sendto("Hello World!".encode(), ( "192.168.190.1" , 8080))

# 关闭套接字
udp_socket.close
~~~



#### 接受信息

![image-20210808193256470](http://sirmegamu.github.io/images/posts/2021-08-11-net_transparent/net_transparent2.png)

~~~python
# 导入模块
import socket

# 创建套接字(使用IPv4,UDP)
udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

# 绑定指定端口8081
udp_socket.bind(("",8081))

# 接受向该端口二进制数据
# （会造成程序的阻塞[类似input()]）
# .recvfrom(接受的字节数,)
recv_data = udp_socket.recvfrom(1024) # 得到一个元组(字符串二进制,(IPv4地址,端口))
print("来自"+str(recv_data[1][0])+"用户"+str(recv_data[1][1])+"端口"+"的消息：")

# 解码得到字符串
# 中国Windows默认使用gbk
text = recv_data[0].decode("gbk")

# 输出显示接收到的内容
print(text)

# 关闭
udp_socket.close
~~~

##### 注意！


注意端口选择的范围！  
尽量不要绑定IP地址，只绑定端口  
这样在计算机有多个网卡时，不同网卡的数据都能被接受

#### 广播

hostID为1的地址是广播地址，  
192.168.190.255地址向192.168.190下的用户进行广播  
255.255.255.255地址向所有用户进行广播

不能直接发送，需要先设置权限，否则会报错

~~~ubuntu
PermissionError: [Errno 13] Permission denied
~~~

应该这样

~~~python
# 导入模块
import socket

# 创建套接字(使用IPv4,UDP)
udp_socket = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)

# 设置广播权限
# udp_socket.setsockopt(套接字，属性，属性值)
#                     当前套接字          广播属性             可以
udp_socket.setsockopt(socket.SOL_SOCKET,socket.SO_BROADCAST,True)

# 发送信息
udp_socket.sendto("你好！".encode("gbk"),("255.255.255.255",8081))

# 关闭套接字
udp_socket.close
~~~


![image-20210809211819478](http://sirmegamu.github.io/images/posts/2021-08-11-net_transparent/net_transparent3.png)

#### UDP聊天器

~~~python
#!/usr/bin/python3
# 程序独立运行时才启动
# 发送信息    send_msg()
# 接受信息    recv_msg()
# 程序主入口  main()

import socket
def send_msg(udp_socket):
    # 获得接受方IP地址
    send_ip = input("请输入接收方的IP地址：")
    # 指定端口号
    send_port = input("请输入接收方的端口：")
    # 获得发送内容
    send_content = input("请输入要发送的内容：")
    # 发送信息
    try:
        udp_socket.sendto(send_content.encode(),(send_ip,int(send_port)))
    except:
        print("发送错误！")
    
def recv_msg(udp_socket):
    # 接收数据
    recv_data = udp_socket.recvfrom(1024)
    # 解码
    try:
        recv_content = recv_data[0].decode()
    except:
        print("解码错误")
    # 输出文本
    print("来自{0}用户{1}端口的信息：".format(recv_data[1][0],recv_data[1][1]))
    print(recv_content)
    
def main():
    # 创建套接字
    udp_soclet = socket.socket(socket.AF_INET,socket.SOCK_DGRAM)
    # 绑定端口
    udp_soclet.bind(("",8080))
    # 进入程序循环
    while True:
    # 打印菜单
        menu ="———————————\n"
        menu+="聊天器菜单\n"
        menu+="1:发送信息\n"
        menu+="2:接受信息\n"
        menu+="3:退出程序\n———————————\n"
        print(menu)
        # 接收用户输入的选项
        select_num = input("请输入选项:")
        print("\n")
        # 判断用户的选择并调用对应的函数
        if int(select_num) == 1:
            print("您选择的是 1：发送信息")
            send_msg(udp_soclet)
        elif int(select_num) == 2:
            print("您选择的是 2：接收信息")
            recv_msg(udp_soclet)
        elif int(select_num) == 3:
            print("您选择的是 3：退出程序")
            print("系统已退出")
            break
        else:
            print("输入错误！")
    # 关闭套接字
    udp_soclet.close
    
# 执行程序    
if __name__ == "__main__":
    main()
    

~~~



<script data-ad-client="ca-pub-3585063968143785" async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
