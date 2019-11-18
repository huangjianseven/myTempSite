---
title: Linux Mint下安装扫描仪驱动
author: 黄俭
date: '2019-11-16'
slug: Linux-mint-Scanner-Drived
categories:
  - Computer
tags:
  - computer
---
1. 扫描仪型号：Epson Perfection V19
   - 官方Linux驱动：iscan-gt-s650-bundle-2.30.4.x64.deb，之前试装了新版本，有问题。还这个老版本好。不过，Epson自带软件中，如果点“配置”，还是会弹出一个对话框。上面的文字是: In order to print, your print system must be able to handle the PNG file format directly. CUPS or Photo Image Print System (version 1.3.1 or later) do this by default.
   
1. 扫描仪软件
    - Linux Mint自带的“扫描易”，非常好用，可以快速得到扫描床的多个页面。
    
1. 再补充
    - 光装iscan老版本还是不行，重启或扫描仪拔插之后无法找到硬件，解决办法是同时装上新版本imagescan，从命令行多执行几次
    
    ```shell
     $ imagescan
    ```
    - 以上方法可以驱动扫描仪，实在不行多拔插几次扫描仪，多执行几次命令
    - 用“扫描易”时，选择第二个V19,不然无法工作
    - 期间装imagescan时还遇到错误
    
     ```shell
      正在解包 imagescan-plugin-gt-s650 (1.0.2-1epson4linuxmint19) ...
dpkg: 依赖关系问题使得 imagescan 的配置工作不能继续：
 imagescan 依赖于 graphicsmagick；然而：
  未安装软件包 graphicsmagick。
    ```
    - 装上graphicsmagick搞定
