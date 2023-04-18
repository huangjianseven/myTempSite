---
title: 信息安全的数学基础之一
author: 黄俭
date: '2023-04-18'
slug: Information-Security-Basis-Math-01
categories:
  - Computer
tags:
  - computer
---
1. 求欧拉函数的C程序。

 ```C
  #include<stdio.h>
  #include<math.h>

  int Phi(int n)
  {
    int ans=n;
    for(int i=2;i<=sqrt(n);i++)
        if(n%i==0)
        {
            ans=ans/i*(i-1);
            while(n%i==0)
                n = n/i;
        }
    if(n>1)
        ans=ans/n*(n-1);
    return ans;
  }

  int main()
  {
    int a;
    scanf("%d",&a);
    int b = Phi(a);
    printf("%d\n",b);

    return 0;
  }

 ```

1. 求乘法逆元的Python程序。

  ```Python
  def gcd(a,b,s):
      if a%b == 0:
          return b,s
        
      q = a//b
      temp = s[1]
      s[1] = s[0]-q*s[1]
      s[0] = temp

      return gcd(b,a%b,s)

  def ModReverse(a,n):
      s = [1,0]
      gcd(a,n,s)
      if s[1]==0:
          return -1
      elif s[1]<0:
          return n+s[1]
      else:
          return s[1]

  a = int(input())
  b = int(input())

  c = ModReverse(a,b)
  print(c)

```

1. 在RSA公钥密码体系中，已经(n,e)为(35,5)，密文c为10，求明文。
    - 解：`$\phi\left(n\right)=24$`, `$d*e\equiv1\ mod \ \phi(n)$`, 求得d=5
    - `$m\ =\ c^d\ mod\ n\ =\ 10^5\ mod\ 35\ =\ 5$`
    - 还原验算：`$c\ =\ m^e\ mod\ n\ =\ 5^5\ mod\ 35\ =\ 10$`
    
1. 模运算公式
    - `$y\ mod\ x\ =\ y-\lfloor\frac{y}{x}\rfloor\cdot x$`
    - 例子：`$-20\ mod\ 7\ =\ -20\ -\lfloor\frac{-20}{7}\rfloor\cdot7=-20+21=1$`
    
1. 对称密码算法之DES