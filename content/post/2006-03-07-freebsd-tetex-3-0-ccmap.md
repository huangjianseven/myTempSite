---
title: 在FreeBSD的teTeX 3.0里用ccmap
author: 黄俭
date: '2006-03-07'
slug: freebsd-tetex-3-0-ccmap
categories:
  - Computer
tags:
  - UNIX
---
ccmap是由南开大学孙文昌老师开发的通过俄国人的cmap包
启用PDFTeX的CID支持，再提供中文支持的TeX工具包。
这样，用PDFTeX生成的PDF文件就可以在Adobe Reader内
搜索中文词、复制出中文。

除了高丽文的cmap文件无法生成，
GB2312,GBK,BIG5,BIG5+,JIS,UTF-8的cmap文件都做好了。
我将makecmap.tex做了一小处修改：Unicode -> unicode

ccmap原始出处：
http://lsec.cc.ac.cn/cgi-bin/viewcvs.cgi/cct/ccmap/

我配置好的包：
http://www2.intron.ac/pubpic/ccmap.tgz