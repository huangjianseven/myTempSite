---
title: Emacs can not work in a non X11 slackware
author: 黄俭
date: '2007-04-21'
slug: emacs-can-not-work-in-a-non-x11-slackware
categories:
  - Computer
tags:
  - Linux
---
When I install Slackware 11.0 without X-Window. I find that I can’t execute emacs in command line. So I look up in Google. Finally, I get the answer:

>installpkg emacs-nox-21.4-i486-1.tgz

```shell
# cd /usr/bin
# rm emacs
# ln -s emacs-21.4-no-x11 emacs
```