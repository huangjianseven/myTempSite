---
title: Linux Mint中/home扩容的一种思路
author: 黄俭
date: '2020-11-12'
slug: linux-mint_Expansion
categories:
  - Computer
tags:
  - Linux
---
1. 由来
  - 以前测试性地把Linux 装在一台笔记本电脑的固态硬盘中，只有约75G的空间，后来发现这个发布版还挺好用的，逐渐成为主力系统，数据用量也随时间膨胀，终于腾挪不开，想扩容一下。
  - 由于我的电脑是双系统，只能从机械硬盘上删除一个Win分区来实现扩容，这其实只是一种挂载而已。主要参考文献\[[^1]\] \[[^bignote]\]
  
1. 准备
    - 安装GParted，然后删除Win中的一个空闲逻辑分区，并格式化为EXT4. 硬盘分区情况如下两图所示。
    
   ![img](http://123.56.98.124:8080/picLIB/upload/15/Gparted_01.png)
    
   ![img](http://123.56.98.124:8080/picLIB/upload/15/Gparted_02.png)
   

[^1]: [ubuntu 添加新分区，并挂载/home](https://www.cnblogs.com/bigben0123/p/12988656.html)
[^bignote]: [Ubuntu 将其他盘挂载到/home的子目录下及其权限问题](https://www.geek-share.com/detail/2712741082.html)
    