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

他这篇文档里还提到Mactex有一个精简版本，就像Miktex那样，只在有需要时下载必要的包。回想当初我装了2G多的完全版Mactex，有点吃了一大块肥肉的感觉。

他的博客里还有一篇[介绍机器学习](http://kapsterio.github.io/slide/mr)的文章，现收藏在这，以后可能会进入这一领域。