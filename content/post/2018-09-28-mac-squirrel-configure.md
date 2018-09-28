---
title: Mac下鼠須管配置簡入繁出
author: 黃儉
date: '2018-09-28'
slug: mac-squirrel-configure
categories:
  - Work
tags:
  - computer
---
這學期剛開學那會，對繁體輸入有點着迷，於是想着在Mac Book Pro上用五筆打繁體字。

沒有想到這個功能我折騰了一兩天，最後怎麼實現的現在還真想不起具體細節。

總之是重裝了一遍鼠須管，然後將`wubi_trad.schema.yaml`這個文件到處複製，包括用戶文件夾和主程序文件夾（`/Library/Input Methods/Squirrel.app/Contents`）。

然後在用戶文件夾中找到default.custom.yaml和default.yaml，

都加入下面代碼段中的最後一行：
```js
  schema_list:
  - schema: wubi86
  - schema: terra_pinyin
  - schema: wubi_pinyin
  - schema: wubi_trad
```

重新佈置，就好了。

另外，還有一個事與主題相關，也在這裏記錄一下。

Windows中RIME輸入法的名字叫小狼毫（Linux下叫中州韻），長久以來五筆都不能反查，忍了很久，今天終於出手解決了。

方法如下：

安裝[袖珍簡化字拼音方案](https://github.com/rime/rime-pinyin-simp)。之前一定有安裝[五筆字型](https://github.com/rime/rime-wubi)吧？！

然後重新佈置。

或手動拷入用戶文件夾後再佈置。