---
title: Python刷题之字符计数
author: 黄俭
date: '2022-09-07'
slug: python-exercise-01
categories:
  - Computer
tags:
  - Python
---

- 编写程序，输入一段英文，统计其中每个英文字母（不区分大小写）的出现次数，按从多到少的顺序输出。

```python
  from collections import defaultdict

  str = input("Please input a string:")

  str = str.lower()

  chars = defaultdict(int)

  for char in str:
      chars[char] += 1

  new_chars = sorted(chars.items(),key=lambda d:d[1], reverse=True)

  for abc in new_chars:
      print("{}, {}".format(abc[0],abc[1]))
 
```
