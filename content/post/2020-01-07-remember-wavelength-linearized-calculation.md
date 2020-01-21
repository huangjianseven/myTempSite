---
title: 回顾波长归一化标定方法
author: 黄俭
date: '2020-01-07'
slug: remember-wavelength-linearized-calculation
categories:
  - Work
tags:
  - doctor
---

1. 首次设计这种方法是在2018年6月份，现在完全想不起来了，只能重新熟悉一遍；

1. 波长归一化程序操作说明，文件名：`xx_single_csv2.py`
    - 先要用Excel将原始标定数据打开，在波长那一栏，改小数点位数为0，然后文件另存为csv格式；
    - `np.loadtxt()`函数中，将文件名改成刚刚得到的csv文件；
    - 肉眼观察有多少个波长点，在程序的矩阵定义`result=np.zeros((1027,3))`中手工改大小；
    - 运行即可，归一化后的结果保存为文件`linearized_001.txt`；
    
1. 光谱数据线性化处理
    - 一共四个文件，分别是
       - calculate_distribution_pattern.py
       - data_linearization.py
       - initialization.py
       - recalculation.py
       
具体操作规程如下：

1. 打开某一未标定的测量数据（我们称之为RAW数据），画折线图，记下正反两个相邻峰的横坐标位置，填入`initialization.py`中(分别是`peak_1`和`peak_2`)，滤色片的相应波长也在该文件中填入

1. 切换到`calculate_distribution_pattern.py`中，运行即可，将得到一个文件，`distribution.txt`，即分布列

1. 再切换到`data_linearization.py`中，`b=np.loadtxt()`里填入你要线性化的原始数据，运行，会输出线性化数据列到文件`linearization.txt`中。（此处将来可改进，根据`b=np.loadtxt()`中导入的原始数据动态改变输出的文件名。）

1. 这一步运行一个支线程序，是在线性化的基础上，利用ZEMAX中得到的波长-光栅摆角曲线，反过来计算线性采样点的波长。运行即可，标定后的结果保存为文件`recalculation.txt`。

这个计算方法的结果，目前还不太准确，需要进一步优化。

1. 实际操作过程

   首先，面对的是最原始的数据，比如下图
   
![](/post/2020-01-07-remember-wavelength-linearized-calculation_files/1650filter_RAW.jpg)

   其中，横坐标代表采样点，纵坐标是探测器光强量化值。
   
   这个方法，首先，还是要计算出扫描光栅微镜的最大扫描角。因此，先根据上图，计算出周期起止点。需要的条件有：
    
    1. 采样频率
    2. 微镜谐振频率
    3. 滤色片两峰之间的距离
    
   我这一组数据，1650滤色片，峰1的位置是1798，峰2的位置是3122，采样频率3M，微镜谐振频率是621.24Hz，微镜编号是TJ_16P0004，先运行initialization.py，得周期起止点为[47:2460]
   
   然后运行calculate_distribution_pattern.py，得到分布列。
   
   再利用分布列，运行data_linearization.py，对其他数据进行测算，得到一个线性化的文件，有四列，包括序号，光强，点数和摆角。今天运行的时候遇到一个错误，将起止点数据类型改为整型就好了。
   
   最后运行recalculation.py进行重新标定。得图如下：
   
   ![](/post/2020-01-07-remember-wavelength-linearized-calculation_files/1404_1.jpeg)
   
   误差不超过1nm