---
title: RStudio和Netlify博客排查故障
author: 黄俭
date: '2022-02-06'
slug: rstudio-netlify-bug-fixed
categories:
  - Computer
tags:
  - computer
---
1. RStudio提示github账号密码不再支持，要求用token来进行access
    - 在github中申请token，详细步骤见[这里](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
    - 在Rstudio中执行一些命令，详细步骤见[这里](https://stackoverflow.com/questions/66065099/how-to-update-github-authentification-token-on-rstudio-to-match-the-new-policy),在这个过程中要贴token的字串（在github中新建时出现，仅一次）
    
     ```shell
      > install.packages("gitcreds")
      > library(gitcreds)
      > gitcreds_set()
     ```
    - 在netlify中deploy不成功，提示Permission denied (publickey)，于是在github对应库的setting中加入netlify的公钥，设为read-only，参考[这里](https://ttys3.dev/post/how-to-deploy-private-repo-to-netlify/)。