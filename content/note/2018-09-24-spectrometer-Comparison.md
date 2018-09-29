---
title: 光谱仪测量对比
author: 黄俭
date: '2018-09-24'
slug: spectrometer-Comparison
categories:
  - Work
tags:
  - Spectrometer
---
这两天用我做的近红外光谱仪测量液体的透射比，实验结果老是不对劲。见下图。
![我的纯水透射率](/note/2018-09-24-spectrometer-Comparison_files/water_transmission_rate_mine.png)

看了两个文献的相关图谱，分别是叶坤涛^[基于 MEMS 微镜的长波近红外光谱仪的设计与实现]的和Tino Pügnre的^[Near-Infrared Grating Spectrometer for Mobile Phone Applications.]。
![叶坤涛论文](/note/2018-09-24-spectrometer-Comparison_files/yie.png)

![IPMS论文](/note/2018-09-24-spectrometer-Comparison_files/mobile.png)

1450nm处是水的吸收，按道理，过了这个点位，透射率应该有大的回升才对。

于是，用TQ公司的irsys1.7光谱仪也测了下。如图

![TQ_irSys](/note/2018-09-24-spectrometer-Comparison_files/water_transmission_rate.png)

与我的光谱仪测量结果差不多，如下图，左边Mine，右边TQ。
![mine_vs_TQ](/note/2018-09-24-spectrometer-Comparison_files/comparion_mine_tq.png)

难道是没有使用蒸馏水的原因（已排除）？

实验数据从[这里](/note/2018-09-24-spectrometer-Comparison_files/20120920.zip)下载。

另算了一下吸光度。代码如下：

```python
from matplotlib.pyplot import *
import numpy as np

RAW1=np.loadtxt(open("i_0.PRN","rb"),delimiter=" ",dtype='float',skiprows=0)
RAW2=np.loadtxt(open("i_1.PRN","rb"),delimiter=" ",dtype='float',skiprows=0)

Wavelength = RAW1[268:1040,0]*1000
I_0 = RAW1[268:1040,1]
I_1 = RAW2[268:1040,1]

transmission_rate = I_0/I_1
absorbance = np.log10(transmission_rate)

plot(Wavelength,absorbance,label='Pure Water')

xlabel('Wavelength(nm)')
ylabel('Absorbance(a.u.)')

grid()
legend(loc='left')
show()
```
我的光谱仪测的纯水吸光度
![Mine](/note/2018-09-24-spectrometer-Comparison_files/Absorbance_mine.png)

TQ公司irSys测的
![TQ](/note/2018-09-24-spectrometer-Comparison_files/Absorbance_TQ.png)

最后再补一张TQ公司光谱仪测的纯水与乙醇吸光度对比图。

![irSys纯水与乙醇吸光度对比](/note/2018-09-24-spectrometer-Comparison_files/Figure1_small.png)

这张图是用Python 3画的，画风跟Python 2.7还是不一样。另外，如果要输出高DPI文件的话，用下面的代码。
```python
plot(Wavelength,absorbance1,label='Pure Water')
plot(Wavelength,absorbance2,label='Ethanol')

xlabel('Wavelength(nm)')
ylabel('Absorbance(a.u.)')

grid(linestyle='--', linewidth=0.5)
legend(loc='upper left')
#show()

savefig('Figure1.png',dpi=300, format='png')
```