---
title: "pandoc文件转换测试"
author: "黄俭"
date: '2018-09-19'
slug: pandoc-file-Conversion
tags: computer
categories: Work
---

Mac系统下试了试pandoc，确实是神器。Markdown转docx非常方便，公式什么的，也干得很利落。但是，我在用xelatex引擎转PDF时却遇到了中文字体方面的问题。

用以下命令可以解决。

`pandoc  --pdf-engine=xelatex -V CJKmainfont="Songti SC" Introduction.md -o test1.pdf`

参见这里[markdown with LaTeX](http://kapsterio.github.io/prductivity/2015/12/27/markdown-with-latex.html)。