---
title: Debian安装PDF虚拟打印机
author: 黄俭
date: '2008-12-25'
slug: debian-pdf-Virtual-printer
categories:
  - Computer
tags:
  - Linux
---

```shell
#apt-get install cups cups-pdf
```

师范学院的apt源最近选日本的比较好，国内的以前的一些源有点问题。

装了之后首先弹出要你设置samba服务器，首先是设置工作组，我设成grouphuang,然后说是如果你的机器以DHCP方式获取IP地址的话，要修改samba的配置文件，WINS之类的。我把图片放在桌面上samba文件夹中了。

附：sources.list文件

```shell
deb ftp://ftp2.jp.debian.org/debian/ testing main #contrib non-free
deb-src ftp://ftp2.jp.debian.org/debian/ testing main #contrib non-free
deb http://security.debian.org/ testing/updates main
```