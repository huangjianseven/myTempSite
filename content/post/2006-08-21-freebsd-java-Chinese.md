---
title: FreeBSD下java中文显示
author: 黄俭
date: '2006-08-21'
slug: freebsd-java-Chinese
categories:
  - Computer
tags:
  - UNIX
---

先要有[fontconfig.properties](http://hjtek.3322.org/pub/fontconfig.properties)文件,然后依照文件内容配置你的字体就可以了。

比如，我的文件中提到/usr/local/share/fonts/zh_CN/TrueType/zysong.ttf，那么你就要在/usr/local/share/fonts下建zh_CN/TureType目录，并创建一个名为zysong.ttf的链接，我是把zysong.ttf链接到/usr/X11R6/lib/X11/fonts/TrueType/simsun.ttf。

好了，可以了。

用这个程序试试：

 ```java
  import javax.swing.JOptionPane;

  public class TestDialog {
  public static void main(String args[]){
  JOptionPane.showMessageDialog(null,
  “你好，欢迎进入Java世界！”,”对话框测试”,JOptionPane.INFORMATION_MESSAGE);}
  }
 ```