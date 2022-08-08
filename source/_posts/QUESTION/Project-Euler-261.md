---
title: Project Euler 261
category:
  - Project Euler
tags:
  - 佩尔方程
mathjax: true
date: 2022-08-05 21:40:26
---

<escape><!-- more --></escape>

# Project Euler 261

## 题目

### Pivotal Square Sums

Let us call a positive integer $k$ a square-pivot, if there is a pair of integers $m > 0$ and $n \ge k$, such that the sum of the $(m+1)$ consecutive squares up to $k$ equals the sum of the $m$ consecutive squares from $(n+1)$ on:

$$(k-m)^2 + \dots + k^2 = (n+1)^2 + \dots + (n+m)^2.$$

Some small square-pivots are

$\begin{aligned}
&\mathbf{4}: 3^2 + \mathbf{4}^2 = 5^2 \\
&\mathbf{21}: 20^2 + \mathbf{21}^2 = 29^2 \\
&\mathbf{24}: 21^2 + 22^2 + 23^2 + \mathbf{24}^2 = 25^2 + 26^2 + 27^2 \\
&\mathbf{110}: 108^2 + 109^2 + \mathbf{110}^2 = 133^2 + 134^2
\end{aligned}$

Find the sum of all **distinct** square-pivots $\le 10^{10}$.

## 解决方案

本题解参考了Thread中的一些内容。

令$N=10^{10}$。根据平方数的前缀和$s(n)=\dfrac{n(n+1)(2n+1)}{6}$，不难将上述方程改写成$s(k)-s(k-m-1)=s(n+m)-s(n)$。整理后得:

$$k^2 (1 + m) - k m (1 + m) - m n (1 + m + n)=0$$

注意到$m>0,n\ge k,$对方程的两边同时除$m(m+1)$，得到

$$\dfrac{k^2}{m}-k-n-\dfrac{n^2}{m+1}=0\qquad(1)$$

由于$n\ge k$，因此$\dfrac{k^2}{m}-k-k-\dfrac{k^2}{m+1}\ge 0$，这给出了关于$m$的上限满足：$2m(m+1)\le k$。因此有$2m(m+1)\le N$。

接下来进一步化简整个方程。构造两个整数$x,t$，满足：

$$
\left \{\begin{aligned}
  &2k=m(x+1)+t\\
  &2n=(m+1)(x-1)+t
\end{aligned}\right.
$$

回代到方程$(1)$中，得到$-m - m^2 - t^2 + m x^2 + m^2 x^2=0$，化简得：

$$m(m+1)(x^2-1)=t^2\qquad(2)$$

令$m=r\cdot p^2,m+1=s\cdot q^2 $，其中$r,s$是一个无平方因数。并且注意，$m$和$m+1$是互质的。因此$rpsq|t$。令$y=\dfrac{t}{rpsq}$，那么将$m,m+1,t$代入方程$(2)$，得到$x^2-1=rsy^2$。将其移项，得到一个[佩尔方程](https://en.wikipedia.org/wiki/Pell%27s_equation)：

$$x^2-rsy^2=1\qquad(3)$$

佩尔方程在66题已经讲过如何计算，此处不赘述。

最终，从小到大枚举$m$，计算出$r,p,s,q$后，代入方程$(3)$解佩尔方程。求出每一对特定解$(x,y)$后，计算出$t=rpsqy$，最终代入到$k=\dfrac{m(x+1)+t}{2}$。计算出每个解时，需要判断$m(x+1)+t$和$(m+1)(x-1)+t$都是偶数，并且前者不超过后者。

## 代码

```py
from tools import int_sqrt, factorization, pell

N = 10 ** 10
M = (-1 + int_sqrt(1 + 2 * N)) // 2
lf = [0]
lg = [0]
for n in range(1, M + 3):
    x, y = 1, 1
    for p, e in factorization(n):
        if e & 1:
            x *= p
        y *= p ** (e >> 1)
    lf.append(x)
    lg.append(y)

st = set()
for m in range(1, M + 1):
    D = lf[m] * lf[m + 1]
    x1, y1 = pell(D)
    x, y = x1, y1
    tmp = lf[m] * lf[m + 1] * lg[m] * lg[m + 1]
    while True:
        t = tmp * y
        kk = m * (x + 1) + t
        if kk > N * 2:
            break
        nn = (m + 1) * (x - 1) + t
        if nn >= kk and nn % 2 == 0 and kk % 2 == 0:
            st.add(kk >> 1)
        x, y = x1 * x + D * y1 * y, x1 * y + y1 * x
ans = sum(st)
print(ans)

```
