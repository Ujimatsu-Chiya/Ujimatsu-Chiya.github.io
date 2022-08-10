---
title: Project Euler 176
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-17 22:21:22
---

<escape><!-- more --></escape>

# Project Euler 176

## 题目

### Right-angled triangles that share a cathetus

The four right-angled triangles with sides $(9,12,15), (12,16,20), (5,12,13)$ and $(12,35,37)$ all have one of the shorter sides (catheti) equal to $12$. It can be shown that no other integer sided right-angled triangle exists with one of the catheti equal to $12$.

Find the smallest integer that can be the length of a cathetus of exactly $47547$ different integer sided right-angled triangles.

## 解决方案

将前几项枚举出来，放入OEIS查询后发现结果为[A046079](https://oeis.org/A046079)。

查询到`FORMULA`一栏，发现如下信息：

```
Let n = (2^a0)*(p1^a1)*...*(pk^ak). Then a(n) = [(2*a0 - 1)*(2*a1 + 1)*(2*a2 + 1)*(2*a3 + 1)*...*(2*ak + 1) - 1]/2. Note that if there is no a0 term, i.e., if n is odd, then the first term is simply omitted. - Temple Keller (temple.keller(AT)gmail.com), Jan 05 2008
```

这说明，如果一个数$n$的分解质因数为$n=2^{e_0}\prod_{i=1}^k p_i^{e_i}$，
那么，包含$n$这个数的勾股数组个数$f(n)$为：

$$
f(n)=
\left \{\begin{aligned}
  &\dfrac{(2e_0-1) \prod_{i=1}^k(2e_i+1)-1}{2}  & & \text{if}\quad e_0>0 \\
  &\dfrac{\prod_{i=1}^k(2e_i+1)-1}{2} & & \text{else}
\end{aligned}\right.
$$

因此，通过$n$的分解质因数枚举$n$即可，枚举时，为使$n$取到的最小，注意当$e_i>e_j$时，那么$p_i<p_j$。对$2$的质数枚举额外枚举。

对于$f(n)$的一些证明：

根据勾股定理$a^2+b^2=c^2$，得到$a^2=(c+b)(c-b)$，那么问题就转化为相当于有多少对$(x,y)$使得$a^2=xy,x<y$。每一对正数$(x,y)$对应着一对正数$(c,b)$。

如果$a$是一个奇数，根据因数个数定理，不难发现答案就是$\dfrac{\prod_{i=1}^k(2e_i+1)-1}{2}$。

如果$a$是一个偶数，那么$c+b$和$c-b$都为偶数，因此需要减去$c+b$和$c-b$中一个为偶数，一个为奇数的情况，也就是有：$\dfrac{(2e_0+1)\prod_{i=1}^k(2e_i+1)-2\prod_{i=1}^k(2e_i+1)-1}{2}$，那么整理得：$\dfrac{(2e_0-1) \prod_{i=1}^k(2e_i+1)-1}{2}$。

## 代码

```py
from tools import get_prime

Q = 47547
ans = -1
pr = get_prime(3, len(bin(Q)) * 2)


def dfs(val: int, f: int, lim: int, w: int):
    global ans
    if (ans != -1 and val > ans) or (w - 1) // 2 > Q:
        return
    if (w - 1) // 2 == Q:
        ans = val
        return
    for i in range(1, lim):
        val *= pr[f]
        dfs(val, f + 1, i, w * (i * 2 + 1))


for k in range(100):
    if ans != -1 and (1 << k) >= ans:
        break
    if k == 0:
        w = 1
    else:
        w = 2 * k - 1
    dfs(1 << k, 0, 66, w)
print(ans)

```
