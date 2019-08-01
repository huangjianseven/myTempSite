---
title: 在新装的Debian 4.0下编译安装MPlayer
author: 黄俭
date: '2007-05-06'
slug: debian-4-mplayer
categories:
  - Computer
tags:
  - Linux
---
配置选项

```shell
./configure –prefix=/usr/local/mplayer –enable-gui –enable-freetype –with-codecsdir=/usr/lib/codes/ –with-win32libdir=/usr/lib/wincodes/ –language=zh_CN
```
但是出现错误:

>Error: X11 support required for GUI compilation

可能是没有安装libgtk2.0-0-dev