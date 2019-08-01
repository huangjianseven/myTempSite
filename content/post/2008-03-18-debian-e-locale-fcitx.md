---
title: 关于Debian在e文locale下安装配置fcitx输入
author: 黄俭
date: '2008-03-18'
slug: debian-e-locale-fcitx
categories:
  - Computer
tags:
  - Linux
---

我用的是debian etch 完全可以在locale为en_US下调出fcitx
gnome桌面系统.

安装fcitx和im-switch：apt-get install fcitx im-switch

如果你运行locale结果如下：

```bash
LANG=en_US.UTF-8
LC_CTYPE=en_US.UTF-8 这一行如果是zh_CN.UTF-8也可以
LC_NUMERIC=”en_US.UTF-8″
LC_TIME=”en_US.UTF-8″
LC_COLLATE=”en_US.UTF-8″
LC_MONETARY=”en_US.UTF-8″
LC_MESSAGES=”en_US.UTF-8″
LC_PAPER=”en_US.UTF-8″
LC_NAME=”en_US.UTF-8″
LC_ADDRESS=”en_US.UTF-8″
LC_TELEPHONE=”en_US.UTF-8″
LC_MEASUREMENT=”en_US.UTF-8″
LC_IDENTIFICATION=”en_US.UTF-8″
LC_ALL=
```

那就不要动了，如果不是用下面这个命令来改变系统locale

```shell
#dpkg-reconfigure locales
```

分别执行下面的命令给出结果来分析一下吧

```shell
$ ls -ahl /etc/alternatives/|grep input
$ ls -ahl /etc/X11/xinit/xinput.d/
$ ls -ahl ~/.xinput.d/
```

如果最后一步出现no such file or directory
则

```shell
$cd $HOME 到你的用户主目录下
$mkdir .xinput.d
$cd .xinput.d
$ln -s /etc/X11/xinit/xinput.d/fcitx en_US
```

直接做链接

修改文件：
/etc/gtk-2.0/gtk.immodules文件，把有关xim的部分改成：

```bash
“/usr/lib/gtk-2.0/2.4.0/immodules/im-xim.so”
“xim” “X Input Method” “gtk20″ “/usr/share/locale” “en:ko:ja:th:zh
```

否则的话，右键可以看到输入法还是default

如果你升级系统了，可能你的/etc/gtk-2.0下没有东西的话就改这个：

>/usr/lib/gtk-2.0/2.10.0/immodule-files.d/libgtk2.0-0.immodules

把有关xim的部分改成：

```bash
“/usr/lib/gtk-2.0/2.10.0/immodules/im-xim.so”
“xim” “X Input Method” “gtk20″ “/usr/share/locale” “ko:ja:th:zh”
```

加上”en:”

ok,现在logout再登录

运行

```shell
im-switch -s fcitx # 设置fcitx为默认输入法，
```

现在就可以用ctrl+space调出输入法了，用鼠标点击fcitx图标“智能拼音”可以切换输入
法（如五笔等），enjoy!

否则如果不行

运行

```shell
$im-switch -c
```

可以显示当前系统可用的输入法

如果有fcitx就选它

这个跟im-switch -s fcitx是一个作用