---
title: Python处理实验数据
author: 黄俭
date: '2018-09-22'
slug: python-data-processing
categories:
  - Work
tags:
  - programming
---
### 测试Markdown里面贴代码

```python
from matplotlib.pyplot import *
import numpy as np

RAW=np.loadtxt(open("20180920.csv","rb"),delimiter=",",dtype='float',skiprows=0)
noise=np.loadtxt(open("noise_50_cal_v2.txt","rb"),delimiter=" ",dtype='float',skiprows=0)

baseline = 0

Wavelength = RAW[:,0]
I_0 = RAW[:,1]
I_1 = RAW[:,2]

transmission_rate = I_1/I_0

plot(Wavelength,I_0,label='$I_0$')
plot(Wavelength,I_1,label='$I_1$($H_2O$)')
plot(noise[:,0],noise[:,1],label='Dark Noise')

xlabel('Wavelength(nm)')

ylabel('Intensity(a.u.)')
title(r'Raw of Halogen & $H_2O$ & Dark Noise' )

grid()
legend(loc='upper right')
show()
```
执行结果如下图，Python版本： 2.7。
![光强三合一](/post/2018-09-22-python-data-processing_files/raw_3_in_one.jpg)
