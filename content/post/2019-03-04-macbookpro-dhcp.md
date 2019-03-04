---
title: MacBookPro无法获取DHCP网络地址的问题
author: 黄俭
date: '2019-03-04'
slug: macbookpro-dhcp
categories:
  - Work
tags:
  - education
---
1. 问题描述
    - 首先，这个问题不是MacBookPro本身带来的，而是使用了明基PD2710QC扩展坞（智能底座）所引发的。
    - 我的Mac装了一个BOOTCAMP Windows 10，在此系统下，智能底座所带的以太网口是可以获取IP地址并顺利上网的。然而，当切换到Mac系统（10.12.6）下时，却始终只能获得169.X.X.X之类的地址，无法连网。
    
2. 折腾过程
    - 用必应搜索了一下，有这类问题的并不多。有一个帖子说要清空Mac中的一些设置然后重启，见[这里](https://forums.macrumors.com/threads/macbook-pro-not-getting-ip-address-via-dhcp.1734179/)。
    - 后来还是在一个中文的页面看到灵感，见[这里](http://blog.sina.com.cn/s/blog_4b089dd40101522g.html)。估计是驱动问题。
    
3. 解决之道
    - 先到Windows下看看网卡的具体型号，查得为Realtek USB GBE Ethernet Family Controller.
    - 提供邮箱地址后下载Mac版驱动。文件很小，180多Kb。
    - 安装，重启，问题解决。
    
![效果图](/post/2019-03-04-macbookpro-dhcp_files/mac_dhcp.png)