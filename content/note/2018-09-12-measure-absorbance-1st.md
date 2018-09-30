---
title: 初测吸光度
author: 黄俭
date: '2018-09-12'
slug: measure-absorbance-1st
categories:
  - Work
tags:
  - Spectrometer
---
今天请张静师妹配了点酒精溶液和葡萄糖溶液，初步测了下吸光度。

步骤如下：

1. 放置空比色皿，测量透射谱，称之为空气参比 `$I_0$`
1. 注入蒸馏水，测其透射谱，此时得到 `$I_1$`
1. 依下式，计算吸光度 `$A$`

`$A = -lg\frac{I_1}{I_0}$`

这次，测了浓度为50%的乙醇（酒精），以及四种不同浓度的葡萄糖溶液，其中3.0mol的葡萄糖并未完全溶解。

下图是纯水，酒精及2.0mol的葡萄糖吸光度对比。

![纯水，酒精及葡萄糖吸光度对比](/note/2018-09-12-measure-absorbance-1st_files/Figure_2.png)

这一图是纯水与四种不同浓度葡萄糖吸光度对比。

![纯水与四种不同浓度葡萄糖吸光度对比](/note/2018-09-12-measure-absorbance-1st_files/Figure_3.png)

这些图感觉跟主流的吸光度谱不一样，需要进一步分析原因。

最后一图代码如下。

```python
from matplotlib.pyplot import *
import numpy as np

RAW0=np.loadtxt(open("i_0.txt","rb"),delimiter=" ",dtype='float',skiprows=0)
RAW_water=np.loadtxt(open("pure_water.txt","rb"),delimiter=" ",dtype='float',skiprows=0)
RAW_G1=np.loadtxt(open("Glucose_1.txt","rb"),delimiter=" ",dtype='float',skiprows=0)
RAW_G2=np.loadtxt(open("Glucose_2.txt","rb"),delimiter=" ",dtype='float',skiprows=0)
RAW_G3=np.loadtxt(open("Glucose_3.txt","rb"),delimiter=" ",dtype='float',skiprows=0)
RAW_G4=np.loadtxt(open("Glucose_4.txt","rb"),delimiter=" ",dtype='float',skiprows=0)

Wavelength = RAW0[:,0]
I_0 = RAW0[:,1] # Intensity of reference
I_water = RAW_water[:,1] # Intensity of pure water
I_G1 = RAW_G1[:,1] # Intensity of glucose 0.5mol
I_G2 = RAW_G2[:,1]
I_G3 = RAW_G3[:,1]
I_G4 = RAW_G4[:,1]

transmission_rate_water = I_0/I_water
absorbance_water = np.log10(transmission_rate_water)

transmission_rate_glucose_1 = I_0/I_G1
absorbance_g1 = np.log10(transmission_rate_glucose_1)

transmission_rate_glucose_2 = I_0/I_G2
absorbance3_g2 = np.log10(transmission_rate_glucose_2)

transmission_rate_glucose_3 = I_0/I_G3
absorbance_g3 = np.log10(transmission_rate_glucose_3)

transmission_rate_glucose_4 = I_0/I_G4
absorbance_g4 = np.log10(transmission_rate_glucose_4)

plot(Wavelength,absorbance_water,label='Pure Water')
plot(Wavelength,absorbance_g1,label='Glucose 0.5mol')
plot(Wavelength,absorbance3_g2,label='Glucose 1.0mol')
plot(Wavelength,absorbance_g3,label='Glucose 2.0mol')
plot(Wavelength,absorbance_g4,label='Glucose 3.0mol undissolved')

xlabel('Wavelength(nm)')
ylabel('Absorbance(a.u.)')

grid(linestyle='--', linewidth=0.5)
legend(loc='lower right')
show()

#savefig('Figure1.png',dpi=300, format='png')
```
原始数据在[这里](/note/2018-09-12-measure-absorbance-1st_files/20180912.zip)下载。