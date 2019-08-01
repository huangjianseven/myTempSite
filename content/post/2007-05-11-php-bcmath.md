---
title: 重新编译PHP以支持bcmath函数
author: 黄俭
date: '2007-05-11'
slug: php-bcmath
categories:
  - Computer
tags:
  - Linux
---
配置选项如下，其实加上一句 –enable-bcmath就OK了。

```shell
 # ./configure –prefix=/usr/local/php –with-apxs2=/home/apache2/bin/apxs –with-mysqli=/usr/bin/mysql_config –with-gd –with-mysql=/usr/include –with-zlib –with-jpeg-dir=/usr/lib –enable-mbstring -with-tiff-dir=/usr/local –with-freetype-dir=/usr/lib/ –enable-bcmath
```