---
title: 修复FreeBSD的Boot Manager
author: 黄俭
date: '2006-05-11'
slug: freebsd-boot-manager
categories:
  - Computer
tags:
  - UNIX
---
有一次，我在机器POST的时候突然断电，致使Boot Manager丢失。当然也有可能是下面的原因：我在FreeBSD下以root运行了zhcon命令，然后机器死机，重启…….
我在FAQ上找到了修复办法，现在摘录如下,以资备忘：

Boot the FreeBSD boot floppy again and go to the Custom installation menu item. Choose Partition. Select the drive which used to contain your boot manager (likely the first one) and when you come to the partition editor for it, as the very first thing (e.g. do not make any changes) select (W)rite. This will ask for confirmation, say yes, and when you get the Boot Manager selection prompt, be sure to select “Boot Manager”. This will re-write the boot manager to disk. Now quit out of the installation menu and reboot off the hard disk as normal.