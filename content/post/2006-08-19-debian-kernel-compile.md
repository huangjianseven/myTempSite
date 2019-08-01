---
title: Debian下编译内核
author: 黄俭
date: '2006-08-19'
slug: debian-kernel-compile
categories:
  - Computer
tags:
  - Linux
---
1、资源准备：
（1）从www.kernel.org下载内核 http://www.kernel.org/pub/linux/kernel/v2.6/linux-2.6.16.tar.bz2并解压缩到/usr/src下的目录:
tar –bzip2 -xvf linux-2.6.16.tar.bz2
（2）安装编译时用到的工具：apt-get install debhelper modutils kernel-package （3）拷贝原来的内核配置文件到新内核的存放文件夹，改名为.config
cp /boot/config-2.6.15.6 /usr/src/linux-2.6.15.6/.config
2、开始配置内核及编译内核
（1）make menuconfig 或者是 make xconfig （X环境下）
（2）make-kpkg clean 做编译准备
（3）make-kpkg –revision huang.1 kernel_image 编译内核安装包
（4）dpkg -i kernel-image-2.6.15.6_10.00.Custom_i386.deb
3、根据实际情况修改/boot

用 make menuconfig 编译之前有一个提示错误：
ncurses-devel 之类的
装上libncurses5-dev就可以了。