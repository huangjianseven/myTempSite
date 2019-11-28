---
title: Linux Mint与Manjaro安装与初步使用心得
author: 黄俭
date: '2019-11-23'
slug: linux-mint-installation-and-configuration
categories:
  - Computer
tags:
  - Linux
---
先前已经将一部分心得写在了[另一处](/post/2019/05/18/linux-installation-gnome/)，这里只是将另一些零星的记忆汇总在一起。

1. 关于中州韻输入法
    - 这个输入法无疑是很好的，特别在Mac或Linux下要用五笔的时候。只是，在Linux下，此方案有两种形态，其一是fcitx-rime，其二是ibus-rime。而我又分别装过两个发行版：Linux Mint和Linux Manjaro，下面就分别说一下两种发行版下RIME的安装与体会。
    
1. Linux Mint下安装fcitx-rime
    - 第一步当然是装fcitx以及fcitx-rime
       
       ```shell
        $ sudo apt-get install fcitx  fcitx-rime
       ```
    - 重启，然后设中州韻为默认输入法
    - 装librime-data-wubi，装此包时，默认会把librime-data-pinyin_simp装上，安装资源在/usr/share/rime-data
    
       ```shell
        $ sudo apt-get install librime-data-wubi
       ```
    - 打开default.yaml文件，schema_list中加上一行: schema: wubi_pinyin
    
       ```shell
        $ cd ~/.config/fcitx/rime
        $ vim default.yaml
       ```
    - 重新部署，按Ctrl + `选择你想要的中州韻输入法，我最喜欢的就是五笔拼音
    - 或者，建立你自己的custom文件
    
       ```shell
        $ cd ~/.config/fcitx/rime
        $ vim default.custom.yaml
       ```
       
    - 加入以下代码
  
         ```shell
               patch:
                 schema_list:
                 - schema: wubi_pinyin
         ```
1. Linux Mint下安装ibus-rime
    - remove fcitx & fcitx-rime
    - configure input using "im-config" command
    - 以前fcitx装的包要卸载干净，包括上面提到的librime-data-wubi, librime-data-pinyin-simp
    - 多安装了一个librime-data-stroke
    - 用上面说的im-config命令之后，会在home目录下生成一个文件，.xinputrc，这个文件加了一行：run_im ibus
    - ibus的快捷键失灵，在Qt程序中输中文还是会出现一个小方框。
    - 现在是提示词竖着显示
    - 虽然没有fcitx好用，但是，可以在Mendeley中输入中文，所以还是不准备换回fcitx。

 [【输入法】Rime-中州韵 基本设置 附：官方定制指南](https://www.cnblogs.com/hellxz/p/10198540.html)
 
[Rime wubi for iMac] (https://blog.csdn.net/hhbgk/article/details/98475939)

[Ubuntu五笔输入终极解决方案(Rime)](https://blog.csdn.net/sacredness/article/details/92195032)


        
