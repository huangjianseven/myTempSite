---
title: Debian4.0下编译安装Apache+PHP+MySQL
author: 黄俭
date: '2007-05-06'
slug: debian4-apache-php-mysql
categories:
  - Computer
tags:
  - Linux
---
MySQL是通过apt-get安装的。
编译Apache的版本是2.0.59
配置如下：

```shell
./configure -enable-so –with-mpm=prefork
```
这个配置一般没有问题，但是最近php官网有一个警告：

> 不推荐将线程化 MPM 用于实际运作的 Apache 2 环境中去。用 prefork MPM 替代，或者用 Apache 1。

我查了FAQ，里面也说得不是很清楚：

>PHP 是粘合剂。它将几十种第三方的库粘合到一起来创建很酷的 web 应用，并通过很直观且易于学习的语言界面使其看上去好像一个整体。PHP 的灵活与强大依赖于底层平台的稳定与耐用。起码需要将一个可运作的操作系统，一个可运作的 web 服务器以及可运作的第三方库粘合起来。其中任何一方不运作了，PHP 都需要有方法来识别出问题并且快速解决。如果没有完全独立的执行线程，完全独立的内存单元和稳定的空间对付每个请求，那底层架构就太复杂以至于不稳定因素更容易进入到 PHP 系统中。

PHP安装之前要确认你是否安装了以下包：（当然啦，根据我的configure来）

 ```shell
  # apt-get install libmysqlclient15-dev
  # apt-get install libfreetype6-dev
  # apt-get install libpng3-dev
  # apt-get install libjpeg-dev
  # apt-get install libz-dev
  # apt-get install libxml2-dev
  # apt-get install bison
  # apt-get install flex
 ```
 
 我的configure如下：
 
 ```shell
 ./configure –prefix=/usr/local/php –with-apxs2=/usr/local/apache2/bin/apxs –with-mysqli=/usr/bin/mysql_config –with-gd –with-mysql=/usr/include –with-zlib –with-jpeg-dir=/usr/lib –enable-mbstring -with-tiff-dir=/usr/local –with-freetype-dir=/usr/lib/
```