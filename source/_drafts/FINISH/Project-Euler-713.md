---
title: Project Euler 713
tags:
  - Project Euler
  - OEIS
  - 图论
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 713

## 题目

### Turán's water heating system

Turan has the electrical water heating system outside his house in a shed. The electrical system uses two fuses in series, one in the house and one in the shed. (Nowadays old fashioned fuses are often replaced with reusable mini circuit breakers, but Turan's system still uses old fashioned fuses.)
For the heating system to work both fuses must work.

Turan has $N$ fuses. He knows that $m$ of them are working and the rest are blown. However, he doesn't know which ones are blown. So he tries different combinations until the heating system turns on.

We denote by $T(N,m)$ the smallest number of tries required to *ensure* the heating system turns on.
$T(3,2)=3$ and $T(8,4)=7$.

Let $L(N)$ be the sum of all $T(N, m)$ for $2 \leq m \leq N$.
$L(10^3)=3281346$

Find $L(10^7)$.

## 解决方案

将$N$条保险丝视为$N$个节点，视作是一个无向图。当一开始的时候，$N$个节点都是两两相邻的。如果两个节点被进行了一次测试，那么就将它们之间的边删除。

可以知道，如果将$m$条能够使用的保险丝两两相连，那么就会形成一个大小为$m$的团。因此按照上面的删边过程，至少要将图删边删到不存在大小为$m$的团。当一个图不存在大小为$m$的团时，那么必定能找到一种解。

那么现在问题就转变成：$N$个节点，至多只能留下多少条边（至少能删去多少条边），使得这个图不存在大小为$m$的团。策略则是将这$N$个节点均匀尽可能相等地均匀划分成$m-1$块，块内的节点不连边，不属于同一块的节点连两条边。[图兰定理](https://en.wikipedia.org/wiki/Tur%C3%A1n%27s_theorem)说明这个图是[图兰图](https://en.wikipedia.org/wiki/Tur%C3%A1n_graph)$T_{N,m-1}.$

图兰定理还给出了图兰图$T_{n,r}$的边数（假设$n=qr+s,0\le s<r$）：

$$(1-\dfrac{1}{r})\dfrac{n^2-s^2}{2}+\dfrac{s(s-1)}{2}$$

那么我们只需要求$T_{N,m-1}$补图边数即为答案。

如果不知道图兰图与图兰定理这些内容，考虑小范围内枚举出一部分项，在OEIS中查询到结果为[A134546](https://oeis.org/A134546)。在FORMULA一栏，找到：

```
T(n,k) = k*floor(n/k)*floor((n+k)/k)/2 - floor(n/k)*(k-1-(n mod k)). - Bob Selcoe, Aug 21 2016
```

那么直接模拟这段式子直接计算$L$即可。

## 代码

```py
N = 10 ** 7
ans = 0
for r in range(1, N):
    q, s = divmod(N, r)
    ans += r * q * (q - 1) // 2 + s * q
print(ans)

```
