---
title: 高中听力错题整理
author: 黄俭
date: '2023-02-15'
slug: English-listening-mark
categories:
  - Family
tags:
  - education
---

高中英语听力的错题，小孩子是没有能力去整理的，所以我想了一个方案来帮助他们。

到今天为止，已经坚持到第五期了。

题目来源：天学网手机APP。

步骤：

1. 用一个安卓手机，在天学网APP播放英语听力时，进行屏幕录制，得到视频。

1. 将视频中的音频用FFMPEG提取出来，命令格式如下：

```shell
 $ ffmpeg -i Screenrecorder-2023-02-12-14-03-02-95.mp4 -vn -c:a libmp3lame -q:a 1 05.mp3
```

1. 用开源的音频编辑软件Audacity，将错题整理成一个MP3，其中一些“叮”的声音，从网站[爱给网](https://www.aigei.com)下载。Audacity一开始还不容易上手，但是把它想像成音频界的Photoshop就可以从它的设计哲学上理解它，就好操作了。

1. 后面做音频有点烦了，就用了B站上土妹老师的视频，地址：[土妹教英语](https://www.bilibili.com/video/BV1sG4y1n7Da)，一共25套题，配套的材料pdf可以在土妹的公众号下载。