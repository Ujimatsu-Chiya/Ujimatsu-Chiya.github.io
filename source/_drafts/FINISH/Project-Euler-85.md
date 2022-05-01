---
title: Project Euler 85
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 17:34:47
---

<escape><!-- more --></escape>

# Project Euler 85
## 题目
### Counting rectangles
By counting carefully it can be seen that a rectangular grid measuring $3$ by $2$ contains eighteen rectangles:

![](../images/p085.png)

Although there exists no rectangular grid that contains exactly two million rectangles, find the area of the grid with the nearest solution.

## 解决方案

对于一个$n\times m$的矩形，每一个小矩形对应着一个行区间的选择$[u,d](1\leq u\leq d \leq n)$，和一个列区间的选择$[l,r](1\leq l\leq r\leq m)$。

注意到，这两个选择是**相互独立**的，行区间和列区间只要有一个不同的选择，那它就对应一个不同的的矩形。

行区间的选择个数为$\dfrac{n(n+1)}{2}$，列区间的选择个数为$\dfrac{m(m+1)}{2}$。

因此，一个$n\times m$的矩形包含了$c(n,m)=\dfrac{n(n+1)m(m+1)}{4}$个小矩形。

直接枚举所有$c(n,m)\leq 2*10^6$的矩形进行判断就可以完成。

## 代码

```py
from itertools import count

N = 2000000


def cal(n, m):
    return (n * (n + 1) * m * (m + 1)) >> 2


mx = 0
for n in count(1, 1):
    if cal(n, 1) > N:
        break
    for m in count(n, 1):
        w = cal(n, m)
        if w > N:
            break
        if w > mx:
            mx = w
            ans = n * m

print(ans)

```