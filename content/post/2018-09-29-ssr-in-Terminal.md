---
title: 在终端也用上SSR
author: 黄俭
date: '2018-09-29'
slug: ssr-in-Terminal
categories:
  - Work
tags:
  - computer
---
有时，在终端执行hugo或下载一些包时，经常会被一个qiang所阻。就在网上搜了下解决办法，希望在Terminal也能顺畅上网。

果然有简易办法，参见[这里](https://github.com/Dream4ever/knowledge-base/issues/55)。

先在终端中用 `curl ip.cn` 检查本机 IP，确认终端目前没有用到代理。

```bash
$ curl ip.cn
当前 IP：*.*.*.* 来自：重庆市 电信
```

由于已在 SSR 客户端软件中设置代理地址为 `socks5://127.0.0.1:1086`，因此在终端中用如下命令，让 HTTP 协议走 SOCKS5：

```bash
$ export http_proxy=socks5://127.0.0.1:1086
```
然后再检查本机 IP，确保代理设置生效：

```bash
$ curl ip.cn
当前 IP：*.*.*.* 来自：日本
```
这个时候，就可以放心地下载 npm 依赖了。下载完成后，在终端中再执行命令 `unset http_proxy`，恢复 HTTP 代理为默认设置。