---
title: Project Euler 183
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>




# Project Euler 183
## 题目
### Maximum product of parts

Let $N$ be a positive integer and let $N$ be split into $k$ equal parts, $r = \dfrac{N}{k}$, so that $N = r + r + \dots + r$.

Let $P$ be the product of these parts, $P = r × r × \dots × r = r^k$.


For example, if $11$ is split into five equal parts, $11 = 2.2 + 2.2 + 2.2 + 2.2 + 2.2$, then $P = 2.2^5 = 51.53632$.

Let $M(N) = P_max$ for a given value of $N$.

It turns out that the maximum for $N = 11$ is found by splitting eleven into four equal parts which leads to $P_{\max} = (\dfrac{11}{4})^4$; that is, $M(11) = \dfrac{14641}{256} = 57.19140625$, which is a terminating decimal.

However, for $N = 8$ the maximum is achieved by splitting it into three equal parts, so $M(8) = \dfrac{512}{27}$, which is a non-terminating decimal.

Let $D(N) = N$ if $M(N)$ is a non-terminating decimal and $D(N) = -N$ if $M(N)$ is a terminating decimal.

For example, $\sum D(N)$ for $5 \le N \le 100$ is $2438$.

Find $\sum D(N)$ for $5 \le N \le 10000$.


## 解决方案

令函数$y(k)=(\dfrac{N}{k})^k$，其中$k\in \mathbb{N^+}$。

由于函数$y(k)$的定义域是在整数域上，不好通过求导求最大值，因此将整数域扩展到实数域。

令$z(x)=(\dfrac{N}{x})^x$，其中$x\in \mathbb{R}$。

对$z(x)$求导，计算得$z$的导数$z'(x)=(\dfrac{N}{x})^x\cdot (\ln\dfrac{N}{x}-1)$。

令$z'(x)=0$，那么可以计算得到$x=\dfrac{N}{e}$，$z(x)$在$x_0=\dfrac{N}{e}$时将会取到最大值。


回到函数$y(k)$，那么如果$y$要取到最大值，那么最大值点$k$为$\lfloor\dfrac{N}{e}\rfloor,\lceil\dfrac{N}{e}\rceil$两个值之一。

因此，直接将它们代入函数$y(k)$代入，这种做法是可行的，不过由于$x_0=\dfrac{N}{e}$是在指数上出现的，因此直接代入计算，可能会导致结果失真。这里取而代之的方法是，代入$y(k)$的对数函数$\ln y(k)=k(\ln N-\ln k)$进行比较计算。

最终找到最大值点$k_0$后，开始解决最大值是否为有限小数的问题。

而这个问题比较简单，只需要判断分数$\dfrac{N}{k_0}$是否为有限小数即可。

## 代码

```py
from math import e, ceil, floor, log, gcd

N = 10000
ans = 0
for n in range(5, N + 1):
    val = n / e
    l, r = floor(val), ceil(val)
    logfl, logfr = l * log(n / l), r * log(n / r)
    if logfl > logfr:
        x = l
    else:
        x = r
    x //= gcd(x, n)
    while x % 5 == 0:
        x //= 5
    while (x & 1) == 0:
        x >>= 1
    if x == 1:
        ans -= n
    else:
        ans += n
print(ans)

```