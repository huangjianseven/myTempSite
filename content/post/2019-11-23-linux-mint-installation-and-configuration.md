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

1. Majanro Gnome中fcitx-rime（中州韻）的安装
    - 初始安装
    
     ```shell
      $ sudo pacman -S fcitx-rime
      $ sudo pacman -S fcitx-im
      $ sudo pacman -S fcitx-configtool
     ```
    - 建一文件并输入以下代码，第三行要不要输入引号，值得商榷
    
    ```shell
     $ sudo vim ~/.xprofile
    ```
    
    ```bash
       export GTK_IM_MODULE=fcitx
       export QT_IM_MODULE=fcitx
       export XMODIFIERS="@im=fcitx"  
    ```
  - 重启一下系统。
  - 桌面右上角出现键盘图标后进行设置，把中州韻输入法加进来，然后重新布署
    - 然后，新建文件，然后输入以下内容
    
    ```shell
     $ cd ~/.config/fcitx/rime
     $ vim default.custom.yaml
    ```
    
    ```bash
        patch:
           schema_list:
             - schema: wubi_pinyin
    ```
  - 重新布署，按Ctrl + `进行设置
  
1. Majanro Gnome中ibus-rime（中州韻）的安装
    - 清除fcitx启动文件~/.xprofile中的内容
    - 卸载以前的fcitx-rime相关包(如果有安装)
    
    ```shell
     $ sudo pacman -R  fcitx-rime
    
    ```
    - 安装ibus
    
    ```shell
     $ sudo pacman -S ibus
    
    ```
    - 清理/usr/share/rime-data的内容
    - 清理~/.config/fcitx/rime的内容
    - 安装ibus和ibus-rime
    - 在.xprofile中加入以下内容
    
    ```bash
     export GTK_IM_MODULE=ibus
     export XMODIFIERS=@im=ibus
     export QT_IM_MODULE=ibus
     ibus-daemon -d -x
    
    ```
    - 重启
    - 然后，ibus-daemon的图标不能显示出来
    - 装ibus-qt,最近github连不上，得科学上网才能装
    
    ```shell
     $ yay -S ibus-qt
    ```
    - 装完重启
    - 进入系统的"区域与语言"输入法设置，把RIME弄出来
    - 这时，会有RIME重新布署的动作，但是会失败，因为/usr/share/下没有rime-data目录，
    - 从另外的机器把rime-data目录原样复制过来，然后重新布署就可以了
    - GNome下想启动ibus-daemon还是不行的，看来Gnome要玩ibus就是这样的，不要想启动daemon，如果想调整字体大小，那就装个GNome的插件吧。
    - 装了文献管理软件mendeley
    - 装了数据处理软件anaconda,但不知道怎么运行
    
    一个链接，可能有助于解决Linux下OpenVPN GUI连接的问题。
    [ExpressVPN installation failed](https://ubuntuforums.org/showthread.php?t=2342534)
    
  - 安装flashplayer插件
  
  ```shell
   $ sudo pacman -S flashplugin
  ```
  
  - wine
  module:load_so_dll failed to load .so lib "/usr/bin/../lib32/wine/winegstreamer.dll.so": libgstvideo-1.0.so.0
  
  - Q9550机子的wine字体安装进度：WINEPREFIX=~/.win32 winetricks cjkfonts corefonts fakechinese

      
  - 安装net-tools，这样才有netstat之类命令
  
  ```shell
   $ sudo pacman -S net-tools
  ```

1. Linux Mint下安装QQ和微信
    - 采用deepin的版本比较好，git装好wine的环境，然后下载一个容器（就是些应用，每个应用使用一个容器）
    - 微信偶尔有个别乱码，特别是在发表情时，这个无伤大雅。刚装好时，无法预览好友发的图片，后来装个包就好了。点[这里](https://www.lulinux.com/archives/1319).
    - 这两个软件装好之后，字体发虚，看着累。解决办法是装文泉驿字体和Windows下的微软雅黑字体。装前者，看[这里](https://www.cnblogs.com/jay998/p/10613208.html)，装后者，看[这里](https://www.cnblogs.com/intervention/p/4020352.html)。这两个步骤完成之后，Linux Mint中的字体设置照装文泉驿字体那个链接去做就可以了。
    - 启动QQ或微信之后，字体是没有啥问题了，可是QQ的聊天框标题是小方框乱码。这时就执行以下命令可解决。参考文献见[这里](https://askubuntu.com/questions/1159838/steam-font-is-all-white-squares)。
    
    ``` shell
     $ sudo apt install ttf-mscorefonts-installer
     $ sudo fc-cache -f
    ```
    下图是系统字体原先的配置，万一想恢复时备忘。
    
    ![](/post/2019-11-23-linux-mint-installation-and-configuration_files/20200304212400.jpg)
    
1. Linux Mint下打开摄像头
    - 参考文献看这里^[Set up a Webcam with Linux, (http://www.linuxintro.org/wiki/Set_up_a_Webcam_with_Linux)]，我的小麦3摄像头没有被驱动，还不知道怎么操作。

1. Linux Mint下近乎完美安装Office 2010
    - 要安装的包，gdiplus, libxml6,corefonts。
    - Windows下的字体要把sim开头的都拷进来

1. Linux Mint下使用小小输入法
    - ibus挂yong，非常给力，什么环境下都能稳定输出中文
    
安装wine时，mono与gecko下载很慢，下面是手动安装方法：

1. 将mono的安装包复制到/usr/share/wine/mono/目录下，[wiki地址](https://wiki.winehq.org/Main_Page)

1. 至于gecko，分为32位版和64位版，路径在~/.cache/wine，[wiki地址](https://wiki.winehq.org/Gecko),这个包和Wine的版本严格相关，我在办公室台式机上的wine版本是强制降级到1.6的，因为微信中文输入的问题。所以下的gecko版本是2.21。如果要在惠普老笔记本上安装，应该下载最新版2.47。

1. 安装mfc42会有错误，看[这里](https://forum.winehq.org/viewtopic.php?t=16479)

1. photoshop cs6的序列号：1330-1058-7438-6699-6715-0898，安装前断网。

1. Wine程序中的中文乱码问题，有一个临时解决方案，启动环境前加env LC_ALL=zh_CN.UTF-8
  
1. Linux Mint下面重设root密码，见[这里](https://www.jianshu.com/p/f22fb29ec53a)

    ```shell
     $ sudo passwd root
    ```
    
1. Linux下解压缩RAR文件
    - 要装p7zip, 或者unrar。我试了前者。
     
     ```shell
      $ sudo apt install p7zip-full p7zip-rar
      $ 7z x  filename.rar
     ```
     
1. Linux下打印机配置的问题
    - 其实就是CUPS的配置，看[这里]( http://www.siguoya.name/pc/home/article/172)
    - Linux下已经装了官方的HP打印机驱动，插上打印机后虽然不能立即打印，但重启一下就可以了

1. Linux下学习PHP
    - [“思过崖”网站](http://www.siguoya.name/pc/home/article/14  )