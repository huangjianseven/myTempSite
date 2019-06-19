---
title: Debain下驱动声卡及理顺包与包之间的关系
author: 黄俭
date: '2006-08-19'
slug: debain-audio-driver
categories:
  - Computer
tags:
  - Linux
---

我的机器配置：
CPU：Pentium4
OS：Debian Linux / kernel 2.6.8
声卡：Intel Corp. 82801EB/ER (ICH5/ICH5R) AC’97 Audio Controller (rev 02)

参考了linuxsir下的[用Alsa驱动声卡的方法](http://www.linuxsir.org/bbs/showthread.php?t=3338)
不过它上面说的东西确实有些陈旧了。

我的操作有所不同：

1. 先用lspci -v看看你的声卡型号，然后安装alsa-base 和 alsa-source

    ```shell
    # lspci -v
    # apt-get install alsa-base
    # apt-get install alsa-source
    ```
2. 运行 alsaconf，选择声卡。

3. 照它上面的方法编译一个alsa-modules的deb包。
4. 安装你编译出来的包，然后再运行alsaconf配置声卡。
5. OK， enjoy your audio in GNU Debian Linux
    - 其实我估计到第2步可能就差不多了，有机会试一下。
6. Debian下理顺安装包之间的关系
    - 用这个命令：
     ```shell
     # apt-get -f install
     ```

