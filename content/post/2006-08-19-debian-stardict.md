---
title: Debian下编译安装StarDict
author: 黄俭
date: '2006-08-19'
slug: debian-stardict
categories:
  - Computer
tags:
  - Linux
---

我用的桌面是KDE，所以先要装

 ```shell
  # apt-get install libgnomeui-dev
 ```
然后，就是：

 ```shell
  # ./configure –prefix=/usr –disable-gnome-support
 ```

注意：–prefix=/usr 这个选项是把StarDict的资源目录设在/usr/share/stardict。而–disable-gnome-support这个选项视你的桌面情况而定。
当然，有可能遇到其它的没有包的情况，装上就是。比如：libxml-parser-perl
最后：

 ```shell
  # make
  # make install
 ```

装完之后运行：
  
 ```shell
  # stardict
 ```
发现不行，哦，没有退出超级用户。:-)
 ```shell
  $ stardict
 ```
这下可以了。
之后，在/usr/share/stardict下建一个子目录dic，然后下一些词典来吧！！
词典一般是a.tar.bz2文件，用这个：
  
 ```shell
  # tar xjvf a.tar.bz2
 ```
哈哈。
哦，最后说一句：
要是你跟我一样不装gnome系统的话，那么选项–disable-gnome-support一定要加，否则就算是前两步都通过了，在make install时还是会遇到问题，会提示找不到stardict-C.omf.out。还有，要注意看源代码包里的INSTALL文件。
可以查字典了，但是一些音标显示不正常 ，这样来一下就可以了：

 ```shell
 # apt-get install ttf-thryomanes
 ```