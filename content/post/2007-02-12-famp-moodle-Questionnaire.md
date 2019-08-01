---
title: FAMP下Moodle的调查问卷
author: 黄俭
date: '2007-02-12'
slug: famp-moodle-Questionnaire
categories:
  - Computer
tags:
  - education
---
前些天我想在我的服务器上使用Moodle，但配置好之后发现在做调查问卷的时候无法显示统计图片。后我在www.moodle.org上找到了答案。原来要在编译PHP的时候加上–with-freetype-dir=/usr/local/include/freetype2选项。