---
title: 如何在Zemax中优化出精确的波长VS扫描角关系
author: 黄俭
date: '2020-01-07'
slug: how-to-calculate-relationship-scanAngle-vs-Wavelength-in-Zemax
categories:
  - Work
tags:
  - doctor
---

1. 三个重要的操作数
   
    - RAID: Ray angle of incidence in degrees
    - RAED: Ray angle of exitance in degrees
    - SUMM：两数相加
    
1. 一些Zemax中的设定
    - 将扫描光栅那个面（surface 6）的转角作为变量
    - 将第8个坐标面(surface 8)的值设为Pickup，scale factor=-1
    - Wav中增加一个值用来浮动计算，每隔100nm取一个

1. 附Zemax中数学运算操作数列表

    | 序号 | 操作数 |       释义       |
    | :--: | :----: | :--------------: |
    |  1   |  SUMM  |     两数相加     |
    |  2   |  OSUM  |     多数相加     |
    |  3   |  QSUM  | 多数的平方和开根 |
    |  4   |  EQUA  |   多数的平均值   |
    |  5   |  DIFF  |     两数相减     |
    |  6   |  PROD  |     两数相乘     |
    |  7   |  PROB  |    乘一个系数    |
    |  8   |  DIVI  |     两数相除     |
    |  9   |  DIVB  |    除一个系数    |
    |  10  |  SQRT  |      开根号      |
    |  11  |  RECI  |      求倒数      |
    |  12  |  SINE  |      正弦值      |
    |  13  |  COSI  |      余弦值      |
    |  14  |  TANG  |      正切值      |
    |  15  |  ASIN  |     反正弦值     |
    |  16  |  ACOS  |     反余弦值     |
    |  17  |  ATAN  |     反正切值     |
    |  18  |  CONS  |   定义一个常数   |
    |  19  |  MAXX  |     求最大值     |
    |  20  |  MINN  |     求最小值     |
    |  21  |  OPGT  |       大于       |
    |  22  |  OPLT  |       小于       |
    |  23  |  OPVT  |       等于       |
    |  24  |  LOGE  | 以e为底的对数值  |
    |  25  |  LOGT  | 以10为底的对数值 |
    |  26  |  ABSO  |     求绝对值     |

1. 模拟结果

    | 波长(nm) | 扫描角(`$^\circ$`) | 入射角 | 衍射角 | 合角   |
    | -------- | ------------------ | ------ | ------ | ------ |
    | 800      | -3.97              | 17.97  | 30.566 | 48.536 |
    | 900      | -3.179             | 17.179 | 31.357 | 48.536 |
    | 1000     | -2.387             | 16.387 | 32.149 |        |
    | 1100     | -1.593             | 15.593 | 32.943 |        |
    | 1200     | -0.797             | 14.797 | 33.739 |        |
    | 1300     | 0                  | 14     | 34.536 |        |
    | 1400     | 0.799              | 13.201 | 35.335 |        |
    | 1500     | 1.601              | 12.399 | 36.137 |        |
    | 1600     | 2.405              | 11.595 | 36.941 |        |
    | 1700     | 3.212              | 10.788 | 37.748 |        |
    | 1800     | 4.021              | 9.979  | 38.557 |        |

1. 线性回归方程
    - `$\phi = 0.008\lambda-10.376$`
    
1. 回归曲线
    
![](/post/2020-01-07-how-to-calculate-relationship-scanAngle-vs-Wavelength-in-Zemax_files/Linear_fit_web.jpg)

1. 参考文献
    
    - https://tableconvert.com/
    - http://blog.sina.com.cn/s/blog_172e2a9ae0102ypbe.html

