---
title: scim in debian
author: 黄俭
date: '2008-12-28'
slug: scim-in-debian
categories:
  - Computer
tags:
  - Linux
---

我用的locale是en_US.UTF-8，根据SCIM的文档说明，装SCIM最好用UTF-8的locale。（你也可以使用GB2312以及GBK的locale，使用scim都一样的，嘿嘿）

对于一个新装好的没有安装SCIM的Debian系统（新的debian安装器选择中文安装后，一边都已经装好了scim），只要

apt-get install scim

就已经安装好SCIM了！当然还不能用。因为SCIM只是一个输入法平台，还要在上面安装输入法（或者码表）。例如，

apt-get install scim-chinese

就可以使用智能拼音输入法了！当然在使用之前还要先配置一下，配置方法很简单，在/etc/X11/Xsession.d/里新建一个名叫95xinput的文件，文件内容如下

/usr/bin/scim -d
XMODIFIERS=”@im=SCIM”
export XMODIFIERS
export GTK_IM_MODULE=scim

保存文件，确认内容无误后，退出X（建议退出X后运行exit命令重新login一次），再进入X的时候就可以用Ctrl+Space调出SCIM了！
就我的试验情况，这样已经可以在xterm里使用SCIM了。

如果你需要其它中文输入法，可以这样

apt-get install scim-tables-zh

这包括了简体中文的五笔、二笔、广东拼音、自然码，和繁体中文的行列、 }頡五代、大易、注音等输入法了。
我现在使用五笔输入法，能输入简繁汉字，词汇也丰富，很好用。

但是现在还不能在基于GTK的软件中调出SCIM，例如我就不能在leafpad里使用SCIM。解决办法很简单，只要安装scim-gtk2-immodule就可以了。

apt-get install scim-gtk2-immodule

安装后无须重启X，只要重新打开基于GTK的软件就可以了，比如我新开一个leafpad，马上就可以使用SCIM了！

这个命令会根据依赖关系自动安装 scim-server-socket, scim-frontend-socket, scim-config-socket，如果没有安装scim，也会自动安装。

以上是中文输入法的安装，因为我也要用到日语输入法，下面也说说如何让SCIM支持日语输入。

如果是使用sid，可以这样

apt-get install scim-anthy anthy

即可完成日语输入法的安装。

我使用的是完全的Sarge，这就没这么方便，但是真的是稳定很多。

在Sarge里可以借助scim-m17n来提供日语输入。scim-m17n实际上提供了二十多种输入法！装好之后输入法列表蔚为壮观。可以在设置里剔除不需要的输入法，SCIM有GUI的设置介面，非常易用，但是设置后有时需要注销一次才能生效。

apt-get install scim-m17n anthy

这样就可以了，但是同时也会自动装上我不喜欢的gdm，可以用dpkg –purge把它删掉。

如果在安装过程有相关包没找到，可以利用以下命令查询包文件名字，这个在stable和testing或者sid中，包文件名可能不一致。

aptitude search scim

就可以搜索出scim输入法的相关包列表。