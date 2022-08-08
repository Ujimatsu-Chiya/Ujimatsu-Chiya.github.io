---
title: Project Euler 86
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-02 16:36:53
---

<escape><!-- more --></escape>

# Project Euler 86

## 题目

### Cuboid route

A spider, $S$, sits in one corner of a cuboid room, measuring $6$ by $5$ by $3$, and a fly, $F$, sits in the opposite corner. By travelling on the surfaces of the room the shortest “straight line” distance from $S$ to $F$ is $10$ and the path is shown on the diagram.

![](../images/p086.png)

However, there are up to three “shortest” path candidates for any given cuboid and the shortest route doesn’t always have integer length.

It can be shown that there are exactly $2060$ distinct cuboids, ignoring rotations, with integer dimensions, up to a maximum size of $M$ by $M$ by $M$, for which the shortest route has integer length when $M = 100$. This is the least value of $M$ for which the number of solutions first exceeds two thousand; the number of solutions when $M = 99$ is $1975$.

Find the least value of $M$ such that the number of solutions first exceeds one million.

## 解决方案

本题不考虑旋转。因此假设该长方体棱长分别为$a,b,c(a\leq b\leq c)$。通过该长方体的平面展开图，不难发现，最短距离$d$一定满足$d^2=(a+b)^2+c^2$，另外两种行走方式（指$(a+c)^2+b^2$和$(b+c)^2+a^2$）一定不是最短的。

因此，可以先枚举$c$的值，再枚举$a+b$的值，在此过程中，判断$(a+b)^2+c^2$是否为平方数即可。

需要注意的是，当$a+b\leq c$，满足$a\leq b$的$(a,b)$对数为$\lfloor\dfrac{a+b}{2}\rfloor$。当$c< a+b\leq 2c$时，满足$a\leq b\leq c$的$(a,b)$对数为$c+1-\lceil\dfrac{a+b}{2}\rceil$。

## 代码

```py
from itertools import count

from tools import is_square

N = 10 ** 6
cnt = 0
c = 1
for c in count(1, 1):
    for ab in range(2, c * 2 + 1):
        if is_square(ab * ab + c * c):
            if ab <= c:
                cnt += ab // 2
            else:
                cnt += c - (ab + 1) // 2 + 1
    if cnt >= N:
        ans = c
        break
print(ans)

```
