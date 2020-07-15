---
title: Todotxt治療拖延症
author: 黃儉
date: '2020-03-07'
slug: todotxt-study
categories:
  - Work
tags:
  - education
---

1. 先從todotxt的命令行開始，網址在[這裏}(https://github.com/todotxt/todo.txt-cli/wiki/User-Documentation)。
     - Mac系統，期間遇到Homebrew的問題，參見[這裏](https://www.jianshu.com/p/b26c7bc14440)。
        ```shell
         $ brew install todo-txt
         $ cp /usr/local/opt/todo-txt/todo.cfg ~/.todo.cfg
        ```
     - Linux下先下載Todo.txt CLI ，然後解壓縮。會得到三個文件：todo.cfg,  todo_completion,  todo.sh。
     - 做一系列的配置，詳見官網。
     
2. 基本命令
    - t ls 列出未完成項目
    - t pri 1 A 將項目1的優先級設爲A
    - t do 1 完成項目A
    - t lsa 列出所有已完成和未完成項目
    - t ls +project 列出和某項目相關的任務