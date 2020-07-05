---
title: Linux Mint下grub切换双系统
author: 黄俭
date: '2020-07-04'
slug: linux-mint-grub-mkconfig
categories:
  - Computer
tags:
  - Linux
---

1. 修改/etc下的文件
```shell
 # vim /etc/default/grub
```

1. 形成grub 配置
```shell
# grub-mkconfig -o /boot/grub/grub.cfg 
```