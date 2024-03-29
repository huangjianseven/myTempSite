---
title: 一个Python网络编程的入门帖子
author: 黄俭
date: '2022-11-23'
slug: python-networking
categories:
  - Computer
tags:
  - Python
---

点击[这里](https://www.cnblogs.com/initcircuit/p/12286859.html).

 - 此文从以下几个方面对Python的网络编程基础进行了描述
     - 基本原理
     - socket模块
     - select模块
     - asyncore模块
     - asynchat模块
     - socketserver模块
 
 - 编码问题
    - 由于网络是以ascii文本格式传输数据的，而在Python3中，所有字符串都是Unicode编码的。 因此，将字符串通过网络发送时必须转码。而从网络收到数据时，也必须进行解码以转换成Python的字符串。
    -  发送时，可使用字符串的encode()方法进行转码，也可直接使用内置的bytes类型。 接收时，可使用字符串的decode()方法进行解码。
     ```python
      # 转码示例
      s.send('Hello world!'.encode('ascii'))    # 方法一：使用encode()转码
      s.send(b'Hello world!')                   #   方法二：直接发送bytes类型（字节序列）

      # 解码示例
      recv_data = s.recv(1024)
      recv_str = recv_data.decode('ascii')      # 使用decode()解码
     ```
    - 以下略，请参考原文。原博主是一个嵌入式系统开发的专家，其博客中有许多电路方面的文章，简直是初学者的宝库。