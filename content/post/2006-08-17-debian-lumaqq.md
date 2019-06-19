---
title: Debian 下lumaqq字体大小的修改
author: 黄俭
date: '2006-08-17'
slug: debian-lumaqq
categories:
  - Computer
tags:
  - Linux
---

进入下面的目录：
 
 ```shell
    # cd /usr/share/themes/Default/gtk-2.0
 ```
打开gtkrc这个文件，加入以下代码：

 ```bash
  include
  “/usr/share/themes/Default/gtk-2.0/gtkrc”
   style “user-font”
   {
    font_name=
    “Bitstream Vera Sans, Simsun 12″
   }
   widget_class “*” style “user-font”
  include “~/.gtkrc.mine”
 ```
 
就可以了