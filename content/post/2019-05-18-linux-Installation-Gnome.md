---
title: 安装Linux桌面版及必要的应用
author: 黄俭
date: '2019-05-18'
slug: linux-Installation-Gnome
categories:
  - Work
tags:
  - computer
---
## 2019年5月下旬Linux桌面工作环境配置笔记(草稿)

PS: 2019年11月16日有更新

教这门课，不能只讲命令行，稍带研究下如何安装配置一个可用的桌面版Linux.

版本：CentOS

1. 拟解决的问题

    - [X] 双系统，Win7+CentOS7，Grub2管理双系统的启动
    - [X] 安装Python3
    - [X] 浏览器中实现Flash
    - [X] 安装RIME输入法，中州韵
    - [X] 安装听歌软件网易云
    - [ ] 安装影音播放器Myplayer
    - [ ] 安装类似几何画板软件GeoGeBra
    - [X] Blogdown
    - [X] 安装Linux Mint
    - [X] 安装腾讯官方新版QQ
    
1. 在实验室的电脑上装CentOS 
   装完启动桌面后花屏，估计是显卡驱动问题。网上找了相关答案，在[这里](https://ask.csdn.net/questions/220757)。用他的方法虽然没有解决问题，但是启发了我。因为我是一块HD6670的显卡，AMD公司出品，又联想到十几年前AMD收购了Ati公司，所以我就装了个xorg-x11-drv-ati.x86_64，重启后问题解决。:-)
1. Linux应用实践课程网站更新故障
    - 传了一个8MB的压缩包（filename.tar.gz）之后，开新帖不更新。删了这个压缩包之后正常。
1. 安装python的Jupyter
    - 这个没有什么可说的，pip网络安装，一定要用豆瓣的源，飞一般的快。
    - 使用感受
        - 现在终于摸到些门道，知道Markdown可以在Notebook里面写了，也可以将一本notebook下载为pdf文件
        - 下载为Pdf时，不支持中文，应该下载为tex文件，或直接将notebook文件转化为tex文件，然后进一步处理。
1. 安装pandoc
     - 从源代码编译安装，过程中使用的是stack，参考[这里](https://pandoc.org/installing.html)。在此过程中出现些错误，主要是因为stack的版本太低的缘故
     - stack的最新安装方式如[官网](https://docs.haskellstack.org/en/stable/install_and_upgrade.html)所示。
     
     ``` bash
     curl -sSL https://get.haskellstack.org/ | sh
     ```
     - 接下来就按照cnblogs上的一篇文章来操作，在[这里](http://www.cnblogs.com/liujiaq/p/5828649.html)。我安装的时候没有完全按照这个来，导致普通用户无法调用pandoc。因为我用root用户操作，安装后，stack  will install the pandoc executable into /root/.local/bin. 这样一来，即使我把这个路径加到PATH中，普通用户也调用不了pandoc程序。

1. 安装五笔输入法
     - 用下面这条命令就可以实现，参考文献在[这里](https://blog.csdn.net/jaray/article/details/82381382)。装后要注销一下才能把输入法加进来 。
     
         `#  yum install ibus ibus-table-wubi `
1. 安装R语言
     - 先加入一个附加软件包的源EPEL, yum install epel-release
     -  yum -y install R
     - 参考文献见[这里](https://blog.csdn.net/jack_nichao/article/details/76559945)
1. 安装RStudio
     - 官网没有针对CentOS的发布版，下了一个RStudio 1.2.1335 - Fedora 19+/RedHat 7+ (64-bit)
     - $ sudo yum install rstudio-1.2.1335-x86_64.rpm -y
     - 参考文献见[这里](http://devopspy.com/linux/install-r-rstudio-centos-7/)
1. 安装Blogdown
     - 一定要Root用户编译下载安装
1. 安装hugo
     - RStudio经常闪退，无奈用R语言环境来装
     - 自动装的版本太高，提示缺少libc++5.so之类的错误，hugo官网找了低版本0.51，替换掉自动安装路径下的hugo，问题解决。
1. 开始建站
    - 建立一个空文件夹
    
     ```shell
      $ mkdir ~/mynewsite
     ```
    - 进入R语言环境并执行以下命令
    
     ```r
     setwd('~/mynewsite')
     blogdown::newsite()
     ```
1. 让站点运作起来
     - R环境下执行
     
     ```r
     blogdown::serve_site() # 此种情况下只能本地浏览
     ```
     - 如果要让本地局域网能看到就按以下操作
        
      ```r
      blogdown::serve_site(host = '0.0.0.0') # 默认监听在4321端口
      ```
     - 客户机浏览器地址为http://192.168.130.12:4321
     - 参考文献见[这里](https://yihui.name/en/2018/09/localhost-0-0-0-0/)
     - CentOS7默认会开启防火墙，从而屏蔽4321端口。如下操作即可
     
     ```shell
     # firewall-cmd --zone=public --add-port=4321/tcp --permanent
     # firewall-cmd --reload
     ```
1. 安装fcitx
1. 让RStudio能够输入中文
     - 这个问题比较难搞，[参考文献1](https://www.csslayer.info/wordpress/fcitx-dev/a-case-study-how-to-compile-a-fcitx-platforminputcontext-plugin-for-a-proprietary-software-that-uses-qt-5/)，[参考文献2](https://forums.debiancn.org/t/topic/1206)，以及[这里](https://bbs.deepin.org/forum.php?mod=viewthread&tid=149730)，还有[这里](https://github.com/JackieMium/my_blog/issues/12)
     - 官网关于QT的编译也应该看一看，点[这里](https://doc.qt.io/qt-5/linux.html)
     - 第一步是确定RStudio使用的QT版本，见下图
     
     <img src="/post/2019-05-18-linux-Installation-Gnome_files/Detect_the_version_of_QT.png" alt="" width="85%"/>
     
     - 我的编译选项
        
         ```shell
          $ ./configure --prefix=/opt/qt5.12.1 -no-openssl -no-opengl
         ```
     - 最后的拷贝稍有不同，可能与新版本的RStudio有关(1.2.5019)
          
         ```shell
           $ sudo cp /opt/qt5.12.1/plugins/platforminputcontexts/libfcitxplatforminputcontextplugin.so /usr/lib/rstudio/plugins/platforminputcontexts/
         ```
     
1. 安装TexLive 2019
    - 参照的文献在[这里](https://www.jianshu.com/p/3b3a6f1f11bc)，注意他的这条命令
    
    ```shell
    $ locate texlive | xargs rm -rf     # 把所有老版本 texlive 文件删除
    ```
    
    - 一定要慎重，我因为是Root执行的，导致Linux系统崩坏。另外，他说的更新宏包，我并没有操作。
1. Linux下测试TexLive
    - 关于CentOS7中的中文字体
       - 敲命令
       
       ```r
       $ fc-list | grep Wen
       ```
       
      可以找到系统中的中文字体
       
       ```shell
       /usr/share/fonts/wqy-zenhei/wqy-zenhei.ttc: WenQuanYi Zen Hei Sharp,文泉驛點陣正黑:style=Regular
       /usr/share/fonts/wqy-microhei/wqy-microhei.ttc: WenQuanYi Micro Hei,文泉驛微米黑:style=Regular
       ```
       
      所以，"WenQuanYi Micro Hei"就成为xelatex时编译tex文件时的字体选项。LaTeX测试代码如下
       
      ```tex
           \documentclass[a4paper,12pt]{article}

             \usepackage{fontspec,xunicode,xltxtra}
             \usepackage{xeCJK}

             \setCJKmainfont{WenQuanYi Micro Hei}

             \begin{document}
             \title{2019年诗词背诵}
             \author{唐伯虎}
            \date{}
             \maketitle

           \section{2019年5月26日}
           \subsection{张继：枫桥夜泊}
            \begin{center}
              月落乌啼霜满天，江枫渔火对愁眠。\\
              姑苏城外寒山寺，夜半钟声到客船。
           \end{center}
          \end{document}
      ```
    - 加入windows中的字体
       - 见参考文献[这里](http://linux-wiki.cn/wiki/LaTeX%E4%B8%AD%E6%96%87%E6%8E%92%E7%89%88%EF%BC%88%E4%BD%BF%E7%94%A8XeTeX%EF%BC%89)，文档稍显陈旧，但有参考性。但是，操作之后Linux系统中的中文字体出现黑体宋体混杂的局面。
       - 另外，我有一个LaTeX模板可以用来写文档，点击[这里](/post/2019-05-18-linux-Installation-Gnome_files/jianhuang_xelatex_template.zip)下载。只在Windows和MacOSX下测试过，Linux下要注意字体问题。
13. Jupyter notebook中的中文转化问题

14. pandoc转化md到tex或pdf的问题 

15. bb编译安装的问题

16. Linux下安装Spyder配置Python科学计算环境的问题
     - 建议配置在服务器上，用MobaXterm去连接
     
17. 参考资料：

     - 安装Python3的，在[这里](https://www.cnblogs.com/mqxs/p/8692870.html)。装的时候没有找到db4-devel这个包。手动下载了libdb4-4.8.30-13.el7.x86_64.rpm和
libdb4-devel-4.8.30-13.el7.x86_64rpm，然后RPM方式装上。

     - Grub2配置双系统启动的，在[这里](https://blog.csdn.net/qq_37359328/article/details/80928007)，按他的步骤，我又被安装了一个内核，不知道怎么回事。
     - Markdown 支持的代码块高亮见[这里](https://blog.csdn.net/shepherd_dirk/article/details/84646379)
     - 安装EPEL源，参考[这里](https://www.cnblogs.com/renpingsheng/p/7845096.html)
     
18. 用Mac的终端ssh登录FreeBSD出错，解决办法
     - ~/.ssh/config中加一行
     
        ```bash
        HostKeyAlgorithms
        ```
     - ssh的登录变为
     
        ```shell
         ssh -oHostKeyAlgorithms=+ssh-dss  huang@192.168.0.237
        ```
     - FreeBSD中挂载Win分区
        - NTFS
          ```shell
           # mount_ntfs -C cp936 /dev/ad0s1 /mnt/C
          ```
        - FAT32
           ```shell
           # mount_msdosfs -L zh_CN.GBK /dev/ad0s7 /mnt/F
           ```
1. Linux中的文献管理软件Me

1. Linux下如何打开相机RAW文件
    - darktable
    - digiKam
    - RawTherapee
    - Photivo
1. Linux下的PhotoShop
    - GIMP
    
1. Linux下安装主题
    - 11 Best Linux Mint Themes. 点[这里](https://linuxhint.com/11_best_linux_mint_themes/)
    - 上述主题中，我对Evopop感兴趣，主要是背景照片太带感
    
1. Linux下如果用Chrome，可以有泼辣修图，或微信网页版插件之类

1. Linux下如果使用B0pass(百灵快传), 需要将CLI文件同路径下的files文件夹设为当前用户所有

 ```shell
  $ sudo chown -R huangjian:huangjian files/
 ```
1. Linux下备份还原用TimeShift
    - 参考文献点[这里](https://linuxhint.com/timeshift_linux_mint_19_usb/)

1. Linux下的pdf阅读和笔记工具
    - skim能用吗？