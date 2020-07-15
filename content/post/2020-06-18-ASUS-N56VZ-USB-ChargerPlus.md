---
title: 华硕N56VZ的快速充电功能
author: 黄俭
date: '2020-06-18'
slug: ASUS-N56VZ-USB-ChargerPlus
categories:
  - Computer
tags:
  - computer
---

现在用回2012年冬天买的电脑，华硕N56VZ，因为它的屏幕看着柔和，久视不累。

但是，快速充电功能总是无法启动，出现弹窗错误，错误信息如下：


```shell
BIOS reporting failed.

GetChargeIcStatus returns false
```

我以为是BIOS中没有开启USB充电，但进入BIOS中发现此选项是正常开启的。后来，在华硕的官网上下载了旧版本的USB Charger Plus 2.09，安装后问题解决。

![](/post/2020-06-18-ASUS-N56VZ-USB-ChargerPlus_files/asus_usb_charger_plus.png)