---
title: Python中numpy庫函數的溢出問題
author: 黃儉
date: '2020-03-07'
slug: python-numpy-over-flow
categories:
  - Computer
tags:
  - programming
---

下面的python程序會產生溢出，出現在Windows版本，python 3.7.4，64位。

```python
import numpy as np

print(np.power(2,31))
```

改成下面的樣子就沒有問題

```python

import numpy as np

print(np.power(2,31)，dtype='int64')
```

Linux下沒有發現異常，版本3.6.8，64位。