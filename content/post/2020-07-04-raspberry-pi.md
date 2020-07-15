---
title: 树莓派4B装CentOS7折腾
author: 黄俭
date: '2020-07-04'
slug: raspberry-pi
categories:
  - Computer
tags:
  - RaspberryPI
---

1. exFAT格式U盘读取

1. 格式化U盘为ext4，并自动挂载

1. 编译安装aircrack-ng
    - 版本1.0 rc4，出现channel -1的问题，不知是程序编译的问题还是USB无线网卡的问题
    - 今天将上面的版本make uninstall，然后编译了1.2 rc5，一切正常，编译过程按官方的说明书进行，点[这里](https://www.aircrack-ng.org/doku.php?id=install_aircrack)。
    ```shell
     # autorecof -i
     #  ./configure 
     # make
     # make install
     # ldconfig
    ```

1. yum安装PHP7.2
    - 有些周折，包括gd库和libraqm
    
1. 配置LAMP并安装WordPress，我参考[这里](https://blog.csdn.net/hwh1996/article/details/90666775)。期间数据库密码莫名其妙丢失，然后参考[这里](https://developer.aliyun.com/article/483579)解决。
    - WordPress初运行时，写文章和编辑文章时卡死，后来装一个经典编辑器，问题解决。
    - WordPress中文路径有问题，不打算改，将每篇文章路径手动设置英文名。

1. yum安装alien
    - 这个包用来将deb包转成rpm包
    - 这个包带出很多依赖，其中就包括python3
    
1. 更新pip，一般用户安装失败，后用root
```shell
 # sudo python3 -m pip install -i https://pypi.douban.com/simple/ -U pip
```
1. 安装python3的一些包
    - numpy,第一次失败，提示要装python3-devel包
    - pillow，第一次失败，后来参照[官网](https://pillow.readthedocs.io/en/latest/installation.html)安装一系列包
    ```shell
     # yum install libtiff-devel libjpeg-devel openjpeg2-devel zlib-devel     freetype-devel lcms2-devel libwebp-devel tcl-devel tk-devel     harfbuzz-devel fribidi-devel libraqm-devel libimagequant-devel libxcb-devel
    ```
    - gpiozero, 这个是对树莓派的简单控制，参考[官网](https://electropeak.com/learn/tutorial-raspberry-pi-gpio-programming-using-python-full-guide/)
    - RPi.GPIO, 这个比上面的gpiozero功能更多
    ```shell
    ```