---
title: 从初中入学到现在小孩成绩排名趋势图
author: 黄俭
date: '2019-05-17'
slug: grades-ranking
categories:
  - Family
tags:
  - education
---
截至2019年11月12日，13次考试，纵坐标为年级排名，还需要努力，争取初二下学期两人都进入年级前50.

![Ranking](/post/2019-05-17-grades-ranking_files/Figure_1.png)

画图源代码（Python）

```python
import matplotlib.pyplot as plt
import numpy as np

GRADE=np.loadtxt(open("grades.txt"),dtype='float',skiprows=0)

exam_times = GRADE[:,0]
haozhe = GRADE[:,1]
sizhe = GRADE[:,2]

l1, = plt.plot(exam_times,haozhe,'r-o')
l2, = plt.plot(exam_times,sizhe,'b-s')

plt.legend(handles=[l1,l2],labels=['Haozhe','Sizhe'])

plt.xlabel('The Exam No.')

plt.ylabel('The Grades Ranking')

plt.axis([0,11,380,40])

#plt.grid()

plt.show()

```

|考试编号| 大双排名      |  小双排名|
|:------:|:-------------:|:--------:|
|       1|            314|150       |
|       2|            186| 271      |
|       3|            175| 169      |
|       4|            56 |  56      |
|       5|            105|166       |
|       6|            235| 195      |
|       7|            140|   118    |
|       8|           99  | 126      |
|       9|           87  |   48     |
|      10|           113 |   19     |