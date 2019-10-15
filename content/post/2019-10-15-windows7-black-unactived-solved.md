---
title: Windows7出现黑屏副本无法激活的解决办法
author: 黄俭
date: '2019-10-15'
slug: windows7-black-unactived-solved
categories:
  - Computer
tags:
  - computer
---
1. 事情起因
    - 小麦3笔记本电脑原来装有双系统，Win7+CentOS7。因为CentOS7作为桌面环境不是很好用，就想换成Linux Mint。这个小麦3有点特殊，配有两块硬盘，一个SSD，一个SATA机械硬盘，C盘装在SSD上。先清理GRUB，然后在Win7的磁盘管理器中删掉Linux分区（位于SSD中）。重启，出现GRUB Rescue，搞不定，用PE盘修复引导区，还是不行。于是不管，强行装Linux Mint，装完之后可以双系统启动，但是Win7变为无法激活的副本，强行被置为黑色桌面背景。试了好多工具，如小马激活工具，KMS等，均无效。
    - 无奈，找出2017年的win7镜像GHO文件，恢复Win的分区，然后再重装一遍Linux Mint，还是一样的问题。
    
1. 解决办法
    - 在Win7中以管理员身份打开命令提示符，输入命令：SLMGR -REARM，然后马上重启。
    - 找下面的激活工具激活。也可以在[这里](/post/2019-10-15-windows7-black-unactived-solved_files/win7activation_downcc.com.zip)下载。
    
    ![搞定黑屏未激活副本问题](/post/2019-10-15-windows7-black-unactived-solved_files/win7_black.jpg)