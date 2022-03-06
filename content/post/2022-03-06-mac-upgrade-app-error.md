---
title: 升级Mac操作系统带来的一些问题
author: 黄俭
date: '2022-03-06'
slug: mac-upgrade-app-error
categories:
  - Work
tags:
  - programming
---

前几天，将Mac的操作系统从10.13 High Sierra升级到10.14 Mojave，目的是想用笔记软件ToT。升级之后遇到两个问题：

 - IINA无法使用
    - 下一个新版本，解决
 - RStudio中的Git Tab页面消失
    - 放狗搜了一下，找到一个页面，标题是"git tab disappeared after OS X upgrade"，见[这里](https://community.rstudio.com/t/git-tab-disappeared-after-os-x-upgrade/67827/3)。按照其中的方法操作，问题解决。
    
     ```shell
      $ xcode-select install
     ```