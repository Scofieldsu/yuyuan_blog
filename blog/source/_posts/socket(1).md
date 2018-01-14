---
title: socket(1)
date: 2016-04-28 20:49:56
categories: python
tags: [socket，tcp，udp]
---
# 网络编程
- 创建通信端点，它使服务器监听请求，一旦一个通信端点已经建立，监听服务可以进入无线循环中，等待客户端的连接并响应他们的请求。

- 套接字最初始为同一主机上的应用程序所创建，使得主机上运行的一个程序与另一个运行的程序进行通信，这就是所谓的进程间的通信。

- 有两种类型的套接字：基于文件的 和面向网络的

- 基于文件的：AF_UNIX  基于网络的：AF_INET     python2.5引入了对特殊类型的linux套接字支持，AF_NETLINK     python2.6中支持透明的进程间通信（TIPC）协议 AF_TIPC


- 有效端口范围0~65535  （小于1024的为系统预留）

- 面向连接的套接字 （虚拟电路或者流套接字）：提供序列化的、可靠的不重复的数据交付，没有记录边界。传输控制协议（TCP）实现，使用SOCK_STREAM作为套接字类型。

- 面向无连接的套接字（数据报类型的套接字）：用户数据报协议（UDP）实现，使用SOCK_DGRAM作为套接字类型。

## 套接字对象方法

### 服务器端套接字函数

socket类型|描述
----------|----
s.bind()  |绑定地址（主机号 端口号对）到套接字
s.listen()|开始TCP监听
s.accept()|被动接受TCP客户端连接，（阻塞式）等待连续的到来
       
### 客户端套接字函数
socket类型|描述
----------|----
s.connect()   |主动初始化TCP服务器连接
s.connect_ex()|connect()函数扩展版本，出错时返回出错码而不是跑出异常
       
### 公共用途的套接字函数
socket类型|描述
----------|-----
s.recv()       |接受TCP数据
s.send()       |发送TCP数据
s.sendall()    |完整发送TCP数据
s.recvfrom()   |接受UDP数据
s.sendto()     |发送UDP数据
s.getpeername()|连接到当前套接字的远端地址（TCP连接）
s.getsockname()|获取当前套接字的地址
s.getsockopt() |返回指定套接字的参数
s.setsockopt() |设置指定套接字的参数
s.close()      |关闭套接字
        
### 面向模块的套接字函数

socket类型|描述
----------|----
s.setblocking()|设置套接字的阻塞与非阻塞模式
s.settimeout() |设置阻塞套接字操作的超时时间
s.gettimeout() |得到阻塞套接字操作的超时时间
        
### 面向文件的套接字函数

socket类型|描述
----------|----
s.fileno()|套接字的文件描述符
s.makefile()|创建一个与套接字关联的文件对象

## 创建TCP服务器的伪代码：
```python
    服务器 tcpSerSock.py
        核心操作如下：
      　　ss = socket()                # 创建服务器套接字
      　　ss.bind()   　　              # 地址绑定到套接字上
      　　ss.listen()                      # 监听连接
             inf_loop:                       # 服务器无限循环
                  cs = ss.accept()       # 接受客户端连接 阻塞式:程序连接之前处于挂起状态
             comm_loop:                 # 通信循环
                  cs.recv()/cs.send()   # 对话 接受与发送数据
             cs.close()                      # 关闭客户端套接字
             ss.close()                      # 关闭服务器套接字 (可选)

```

## 创建tcp服务器
```python

 # -*- coding: utf-8 -*-
 from socket import *
 from time import ctime

 HOST = 'localhost'          #主机名
 PORT =  21567               #端口号
 BUFSIZE = 1024              #缓冲区大小1K
 ADDR = (HOST,PORT)

 tcpSerSock = socket(AF_INET, SOCK_STREAM)
 tcpSerSock.bind(ADDR)       #绑定地址到套接字
 tcpSerSock.listen(5)        #监听 最多同时5个连接进来

 while True:                 #无限循环等待连接到来
     try:
         print 'Waiting for connection ....'

         tcpCliSock, addr = tcpSerSock.accept()  #被动接受客户端连接
         print u'Connected client from : ', addr

         while True:
             data = tcpCliSock.recv(BUFSIZE)     #接受数据
             if not data:
                 break
             else:
                 print 'Client: ',data
             tcpCliSock.send('[%s] %s' %(ctime(),data)) #时间戳

     except Exception,e:
         print 'Error: ',e
 tcpSerSock.close()          #关闭服务器

```

## 创建tcp客户端的伪代码

```python 
客户端 tcpCliSock.py
        核心操作如下：
      　　cs = socket()                 # 创建客户端套接字
             cs.connect()                  # 尝试连接服务器
             comm_loop:                 # 通讯循环
                  cs.send()/cs.recv()    # 对话 发送接受数据
             cs.close()                       # 关闭客户端套接字

```


## 创建tcp客户端

```python

 # -*- coding: utf-8 -*-
 from socket import *

 HOST = 'localhost'          #主机名
 PORT =  21567               #端口号 与服务器一致
 BUFSIZE = 1024              #缓冲区大小1K
 ADDR = (HOST,PORT)

 tcpCliSock = socket(AF_INET, SOCK_STREAM)
 tcpCliSock.connect(ADDR)    #连接服务器

 while True:                 #无限循环等待连接到来
     try:
         data = raw_input('>')
         if not data:
             break
         tcpCliSock.send(data)            #发送数据
         data = tcpCliSock.recv(BUFSIZE)  #接受数据
         if not data:
             break
         print 'Server: ', data
     except Exception,e:
         print 'Error: ',e

 tcpCliSock.close()          #关闭客户端

```

## 创建udp服务端的伪代码

```python

服务器 udpSerSock.py
        核心操作如下：
      　　ss = socket()                # 创建服务器套接字
      　　ss.bind()   　　              # 绑定服务器套接字
             inf_loop:                       # 服务器无限循环
                  cs = ss.recvfrom()/ss.sendto()
                                                  # 对话 接受与发送数据
             ss.close()                      # 关闭服务器套接字

```


## 创建udp服务端

```python

 # -*- coding: utf-8 -*-
 from socket import *
 from time import ctime

 HOST = ''                   #主机名
 PORT =  21567               #端口号
 BUFSIZE = 1024              #缓冲区大小1K
 ADDR = (HOST,PORT)

 udpSerSock = socket(AF_INET, SOCK_DGRAM)
 udpSerSock.bind(ADDR)       #绑定地址到套接字

 while True:                 #无限循环等待连接到来
     try:
         print 'Waiting for message ....'
         data, addr = udpSerSock.recvfrom(BUFSIZE)          #接受UDP
         print 'Get client msg is: ', data
         udpSerSock.sendto('[%s] %s' %(ctime(),data), addr) #发送UDP
         print 'Received from and returned to: ',addr

     except Exception,e:
         print 'Error: ',e
 udpSerSock.close()          #关闭服务器

```


## 创建udp客户端的伪代码

```python

客户端 udpCliSock.py
        核心操作如下：
      　　cs = socket()                            # 创建客户端套接字
             inf_loop:                                  # 服务器无限循环
                  cs.sendto()/cs.recvfrom()   # 对话 接受与发送数据
             cs.close()                                 # 关闭客户端套接字


```

## 创建udp客户端

```python

 # -*- coding: utf-8 -*-
 from socket import *

 HOST = 'localhost'          #主机名
 PORT =  21567               #端口号 与服务器一致
 BUFSIZE = 1024              #缓冲区大小1K
 ADDR = (HOST,PORT)

 udpCliSock = socket(AF_INET, SOCK_DGRAM)

 while True:                 #无限循环等待连接到来
     try:
         data = raw_input('>')
         if not data:
             break
         udpCliSock.sendto(data, ADDR)            #发送数据
         data,ADDR = udpCliSock.recvfrom(BUFSIZE)  #接受数据
         if not data:
             break
         print 'Server : ', data

     except Exception,e:
         print 'Error: ',e

 udpCliSock.close()          #关闭客户端

```
