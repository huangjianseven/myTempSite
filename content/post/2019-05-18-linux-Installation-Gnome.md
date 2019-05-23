---
title: 安装Linux桌面版及必要的应用
author: 黄俭
date: '2019-05-18'
slug: linux-Installation-Gnome
categories:
  - Work
tags:
  - computer
---
教这门课，不能只讲命令行，稍带研究下如何安装配置一个可用的桌面版Linux.

版本：CentOS

解决的问题：

1. 双系统，Win7+CentOS7，Grub2管理双系统的启动
2. 安装Python3
3. 浏览器中实现Flash
4. 安装RIME输入法，中州韵
5. 安装听歌软件网易云
6. 安装影音播放器Myplayer
7. 安装类似几何画板软件
8. Blogdown

参考资料：

1. 安装Python3的，在[这里](https://www.cnblogs.com/mqxs/p/8692870.html)。装的时候没有找到db4-devel这个包。手动下载了libdb4-4.8.30-13.el7.x86_64.rpm和
libdb4-devel-4.8.30-13.el7.x86_64rpm，然后RPM方式装上。

2. Grub2配置双系统启动的，在[这里](https://blog.csdn.net/qq_37359328/article/details/80928007)，按他的步骤，我又被安装了一个内核，不知道怎么回事。

3. 在实验室的电脑上装CentOS 7，装完启动桌面后花屏，估计是显卡驱动问题。网上找了相关答案，在[这里](https://ask.csdn.net/questions/220757)。用他的方法虽然没有解决问题，但是启发了我。因为我是一块HD6670的显卡，AMD公司出品，又联想到十几年前AMD收购了Ati公司，所以我就装了个xorg-x11-drv-ati.x86_64，重启后问题解决。:-)

4. linux course update problem