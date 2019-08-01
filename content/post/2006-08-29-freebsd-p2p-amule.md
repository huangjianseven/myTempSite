---
title: FreeBSD下安装P2P下载软件aMule
author: 黄俭
date: '2006-08-29'
slug: freebsd-p2p-amule
categories:
  - Computer
tags:
  - UNIX
---

首先要编译安装wxGTK，步骤如下（参考[here](http://www.amule.org/wiki/index.php/Compilation_Installation#Manual_Installation)）：
第一步：
下载 wxGTK的两个包：

wxGTK-2.6.3.tar.bz2
wxWidgets-2.6.3-Patch-2.tar.gz

然后 Compile wxGTK

 ```shell
  # tar -jxvf wxGTK-2.6.3.tar.bz2
  # tar -C wxGTK-2.6.3 -xzvf wxWidgets-2.6.3-Patch-2.tar.gz
  # cd wxGTK-2.6.3
  # ./configure –prefix=/usr –with-gtk –enable-unicode –disable-compat24 –enable-optimise && make
 ```
As root:

 ```shell
  # make install
  # ldconfig
 ```
第二步, 下载aMule的最新源码包：

* Download the latest aMule version 

* Compile aMule (please check the configure article) 
   
  ```shell
   # tar -zxvf aMule-X.X.X.tar.gz (replace X with the right version number..)
   # cd aMule-X.X.X
   # ./configure –disable-debug –enable-optimize && make
  ```
* As root:

 ```shell
  # make install
 ```
* Run aMule as a regular user from console by typing -> amule

不忘记在FreeBSD下要用gmake