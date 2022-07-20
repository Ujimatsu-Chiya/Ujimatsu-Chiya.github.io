---
title: Project Euler 394
tags:
  - Project Euler
  - 概率
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 394
## 题目
### Eating pie



Jeff eats a pie in an unusual way.

The pie is circular. He starts with slicing an initial cut in the pie along a radius.
While there is at least a given fraction $F$ of pie left, he performs the following procedure:

- He makes two slices from the pie centre to any point of what is remaining of the pie border, any point on the remaining pie border equally likely. This will divide the remaining pie into three pieces.

- Going counterclockwise from the initial cut, he takes the first two pie pieces and eats them.

When less than a fraction $F$ of pie remains, he does not repeat this procedure. Instead, he eats all of the remaining pie.

![](../images/p394_eatpie.gif)

For $x \ge 1$, let $E(x)$ be the expected number of times Jeff repeats the procedure above with $F = \dfrac{1}{x}$.

It can be verified that  $E(1) = 1, E(2) \approx 1.2676536759,$ and $E(7.5) \approx 2.1215732071$.

Find $E(40)$ rounded to $10$ decimal places behind the decimal point.



## 解决方案

本解决方案参考了Thread的一些内容。

令$F=\dfrac{1}{40}$。令$f(r)(0\le r\le 1)$表示当前仍然剩下比率为$r$的派时，需要进行的轮数的期望。那么当$r< F$时，$f(r)=0$。否则按照期望动态规划的思想，$f(r)$可以写成

$$f(r)=\dfrac{1}{r^2}\int_0^r\int_0^r(1+f(\min(r_1,r_2)))dr_1dr_2$$

由于每一轮中切的两刀是**独立**的，那么逆时针剩下的一部分就是两次剩余比率中的较小值。这个方程第一步可以化简为：

$$r^2f(r)=r^2+\int_0^r\int_0^rf(\min(r_1,r_2))dr_1dr_2$$

目前只考虑右边的积分部分，可以发现，积分区域是独立对称的。假设$r_1\le r_2$，那么可以改写成

$$\begin{aligned}
\int_0^r\int_0^rf(\min(r_1,r_2))dr_1dr_2&=2\int_0^r\int_{r_1}^rf(r_1)dr_2dr_1\\
&=2(r\int_0^rf(r_1)dr_1-\int_0^rr_1f(r_1)dr_1)\\
&=2(r\int_F^rf(x)dx-\int_F^rxf(x)dx)
\end{aligned}$$

重新代入上式，那么我们就得到了一个关于$f(r)$的积分方程：

$$r^2f(r)=r^2+2(r\int_F^rf(x)dx-\int_F^rxf(x)dx)\qquad(1)$$

将其转化成微分方程求解。那么两边对$r$求一次导得到：

$$r^2f'(r)+2rf(r)=2r+2(\int_F^rf(x)dx+rf(r)-rf(r))$$

化简后，两边再对$r$求一次导，最终化简得到：

$$r^2f''(r)+4rf'(r)=2$$

在Mathematica中使用如下代码解上面的微分方程：

```Mathematica
DSolve[r^2*f''[r] + 4 r *f'[r] == 2, f[r], r]
```

最终得到这个微分方程的通解$f(r)$为：

$$f(r)=\dfrac{\ln r}{3}-\dfrac{c_1}{3r^3}+c_2\qquad(2)$$

将$(2)$回代到$(1)$，利用恒等的性质，并令$x=\dfrac{1}{F}$，最终得到：

$f(r)=\dfrac{1}{9}(\dfrac{2}{x^3r^3}+6\ln xr+7)$

那么$f(1)$就是所求值，$E(x)=\dfrac{2x^3}{9}+\dfrac{2\ln x}{3}+\dfrac{7}{9}$
## 代码


```py
from math import log

X = 40
ans = 2 / 9 / X ** 3 + 2 * log(X) / 3 + 7 / 9
print("{:.10f}".format(ans))

```