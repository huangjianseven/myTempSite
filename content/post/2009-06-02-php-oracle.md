---
title: php与oracle(一)
author: 黄俭
date: '2009-06-02'
slug: php-oracle
categories:
  - Computer
tags:
  - programming
---
按照官网的流程,可以让PHP连接到ORACLE,完成一些数据的插入与查询。

但是有一个问题，那就是无法再启动sqlplus了。

后来我解决了这个问题，其实不要在系统变量里加上什么路径，甚至不要设什么tnsnames.ora之类的用户变量。就可以了。连orcl无法识别这样的问题也一并解决了。

但是有一个疑问：客户端中那个大DLL文件有什么用呢，我现在并没有用到它也可以连接到ORACLE。