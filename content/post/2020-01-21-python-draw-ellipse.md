---
title: python画椭圆的方法
author: 黄俭
date: '2020-01-21'
slug: python-draw-ellipse
categories:
  - Computer
tags:
  - computer
---
1. 先传一张效果图

     ![](/post/2020-01-21-python-draw-ellipse_files/Figure_1.png)
  
1. 贴代码

   ```python
    import matplotlib.pyplot  as plt
    import numpy as np

    from matplotlib.pyplot import MultipleLocator


    #第一圈
    phi_max = 4
    voltage_max = 0.8

    x = np.linspace(-1.0*voltage_max,voltage_max,1000)
    y = np.linspace(-1.0*phi_max,phi_max,1000)

    x1 = x*1.0/voltage_max
    y1 = y*1.0/phi_max

    x1,y1 = np.meshgrid(x1,y1)

    # 第二圈

   phi_max2 = 3.5
   voltage_max2 = 0.65

   a = np.linspace(-1.0*voltage_max2,voltage_max2,1000)
   b = np.linspace(-1.0*phi_max2,phi_max2,1000)

   a1 = a*1.0/voltage_max2
   b1= b*1.0/phi_max2

   a1,b1 = np.meshgrid(a1,b1)

  plt.rcParams['xtick.direction'] = 'in'#将x轴的刻度线方向设置向内
  plt.rcParams['ytick.direction'] = 'in'#将y轴的刻度方向设置向内

  ax=plt.gca()

  y_major_locator=MultipleLocator(1)
  ax.yaxis.set_major_locator(y_major_locator)

  plt.ylim(-5,5)



   bx=plt.gca()
   x_major_locator=MultipleLocator(0.2)
   bx.xaxis.set_major_locator(x_major_locator)

   plt.xlim(-1.0,1.0)

   plt.xlabel('Voltage [V]')
   plt.ylabel('Angle [°]')

   # 开始画第一圈

   CS1 = plt.contour(x, y, x1**2 + y1**2, [1]) 


   labels = ['$\phi_{max}=4$°']

   for i in range(len(labels)):
      CS1.collections[i].set_label(labels[i])

   # 开始画第二圈

   CS2 = plt.contour(a, b, a1**2 + b1**2, [1], colors='red') 


   labels = ['$\phi_{max}=3$°']

   for i in range(len(labels)):
      CS2.collections[i].set_label(labels[i])

   plt.grid(color='b', linestyle='--', linewidth=0.5)
   plt.legend(loc='best')
   plt.show()

```
1. 参考文献

      [python绘制圆和椭圆](https://www.cnblogs.com/yibeimingyue/p/9916048.html)
      [How do you create a legend for a contour plot in matplotlib?
](https://stackoverflow.com/questions/10490302/how-do-you-create-a-legend-for-a-contour-plot-in-matplotlib)