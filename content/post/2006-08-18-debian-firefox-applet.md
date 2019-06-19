---
title: Debian下让Firefox支持Applet
author: 黄俭
date: '2006-08-18'
slug: debian-firefox-applet
categories:
  - Computer
tags:
  - Linux
---

假如你已经安装JDK，那么只需进入你的Firefox目录，找到plugins文件夹。在该文件夹中建一个文件链接即可。代码如下：

 ```shell
   # ln -s /usr/local/java/jdk1.5.0_08/jre/plugin/i386/ns7/libjavaplugin_oji.so libjavaplugin_oji.so
 ```
如果要测试你的Firefox是否已经支持Applet，点[这里](http://java.sun.com/features/1998/05/birthday.html)。