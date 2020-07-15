---
title: Linux下使用Wine
author: 黄俭
date: '2019-12-08'
slug: linux-using-wine
categories:
  - Computer
tags:
  - computer
---

## 缘起

一直想打造一个Linux的桌面环境，而一些Windows下的常用软件却是绕不开的存在。比如Photoshop和Office等。

还好，经过这些年来的发展，Wine已经能够较好的运行一些Win版程序，它不是模拟器，而是一个兼容层，官网在[这里](https://www.winehq.org/)。

## 安装

1. 我的发行版
    - 经过一段时间的试用，我Manjaro和Mint之间，我还是选择了后者，原因有二。
       - Manjaro的Gnome版无法加载小小输入法（或许是我还没有找到办法）。而小小输入法能够在Office中移动面板。
       - Manjaro太过激进，软件总是要装最新版。比如Wine，我装个稳定版就可以了。
       
1. 主要参考文献
    - 除了官方网站，我的第一参考是[[Linux]使用Wine](https://blog.csdn.net/buildcourage/article/details/80871141)，然后便是
    
1. 安装PhotoShop CS6
    - 网上下的一些安装包往往会崩溃在初始化阶段，用大眼仔提供的Extended版就没有这个问题
    
1. 安装Office 2007和Office 2010
    - 这两个软件都能正常安装，Office2010的激活可能要麻烦一点。参考[这里](http://www.sohu.com/a/162185166_295478)和[这里](https://ubuntuforums.org/showthread.php?t=1885051)。
    - samba和winbind, dotnet20、msxml6以及核心字体必须安装。gdiplus也很重要。
    - 目前使用中遇到的问题
       - PowerPoint在放映时会有显卡不兼容的提示，然后放映确实会出现卡滞或花屏的现象，有时软件甚至会不响应。
       - Word有时会提示normal.dot，模板类报警，然后无法打开本机上的文件。这时，找一个本地文件，右键使用Wine Office Word打开试试。
       - 在卸载软件后，Wine开始菜单的的东西不被清除，那就手动吧。路径在下面。
       
       ```shell
        $ cd ~/.local/share/applications/wine/Programs/
       ```
    
1. 安装QQ与微信
    - 目前用的是deepin版本的QQ与微信，官网在[这里](https://github.com/wszqkzqk/deepin-wine-ubuntu)，开发者在做这个的时候还未成年，太厉害了.
    - 微信装上后不能预览图片，装一个包就可以了( libjpeg62:i386)，参考文献见[这里](https://www.lulinux.com/archives/1319)。
    - 官网还有些其他软件，比如Foxmail和WinRAR之类。
    
## 其他选择

1. CrossOver
    - 这是一个Wine的商业版本，花费不多，却能省掉些琢磨的时间。见[这里](https://raymii.org/s/tutorials/Office_2013_and_2010_on_Linux.html#toc_4)，Linux版和Mac版都有。