---
title: Blogdown搭建个人博客完成
author: 黄俭
date: '2018-09-19'
slug: blogdown-create-website
categories:
  - Work
tags: []
---
昨天晚上到今天上午，都想依样画葫芦，把博客搞成自己理想中的样子。

首先，我克隆了谢大神的站点。接着，我琢磨着想在自己的站点上实现类似的一些效果。但是，失败了。因为，他那个还是太复杂，无法简单模仿。当然了，主要是自己的相关知识太缺乏。

最后，还是回到昨天晚上的版本，只不过现在能够通过git更新了。

给我巨大帮助的资料有钟浩光写的[用 R 语言的 blogdown+hugo+netlify+github 建博客](https://cosx.org/2018/01/build-blog-with-blogdown-hugo-netlify-github/)

还有，当我始终上传不了站点到github的仓库时，看到了shiren1118写的[github上的版本和本地版本冲突的解决方法](https://blog.csdn.net/shiren1118/article/details/7761203).

最后，是谢大神写的书[blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)

以后，多写博文，并搜集自己散落在Web上各个角落的文字，统一汇总到本站。

目前域名：http://huangjianzone.netlify.com

Hugo version: 0.48

以上工作是在Mac系统上完成的，Windows下幺蛾子比较多，遇到的有以下：

1. 经常无法调出中文输入法
1. 刚开始建站时执行`blogdown::install_hugo`时，遇到错误，信息为
    - `Error in file(con, "r") : cannot open the connection
In addition: Warning message:
In file(con, "r") : InternetOpenUrl failed: '无法与服务器建立连接'`

后来，手工安装Hugo解决，参考文档见[这里](https://github.com/rstudio/blogdown/issues/244)。

各版本Hugo在[这里](https://github.com/gohugoio/hugo/releases)下载。
