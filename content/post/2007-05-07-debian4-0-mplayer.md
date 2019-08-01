---
title: Debian4.0下编译安装MPlayer
author: 黄俭
date: '2007-05-07'
slug: debian4-0-mplayer
categories:
  - Computer
tags:
  - Linux
---
装libgtk2.0 dev

装xorg dev

取消esd

essential-20061022.tar.bz2解压放在/usr/local/lib/codecs下面

我的configure

```shell
# ./configure –with-codecsdir=/usr/local/lib/codecs/ –with-win32libdir=/usr/lib/wincodes/ –enable-gui –enable-freetype –language=zh_CN –prefix=/usr/local/mplayer/
```

安装皮肤：

>我用的皮肤是PowerPlayer-1.1.tar.bz2

>注意要ln -s PowerPlayer default

中文字幕

看我的贴图

![](/post/2007-05-07-debian4-0-mplayer_files/Mplayer1.png)

![](/post/2007-05-07-debian4-0-mplayer_files/Mplayer2.png)

还有，编辑你的~/.mplayer/config

因为我的是宽屏显示器，所以加上一句:

monitoraspect=16:9

其实中文字幕问题困挠了我很久，可能有两个小时。
我先是在~/.mplayer/config里面加上这两句

```shell
font=/usr/share/fonts/truetype/arphic/simhei.ttf
subcp=cp936
```

然后复制一个simhei.ttf到/usr/share/fonts/truetype/arphic/下面

```shell
# chmod 644 simhei.ttf
```

再按贴图里面的设置。就可以显示中文字幕了。
之后，删掉~/.mplayer/config里面的那两行
font=/usr/share/fonts/truetype/arphic/simhei.ttf
subcp=cp936
也没有问题，换其它字体也没有问题。

此前虽然按贴图中的设置，却不管用，不知道啊。
可能的原因是：
这一句subcp=cp936，把mplayer首选项->字幕和OSD里面的编码改成了cp936