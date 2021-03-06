---
title: Project Euler 58
tags:
  - Project Euler
mathjax: true
date: 2022-04-26 00:41:50
---


<escape><!-- more --></escape>

# Project Euler 58

## 题目

### Spiral primes

Starting with 1 and spiralling anticlockwise in the following way, a square spiral with side length 7 is formed.
<center style="font-family:'Courier New', monospace;">
<font color=red>37</font> 36 35 34 33 32  <font color=red>31</font> <br /> 38 <font color=red>17</font> 16 15 14 <font color=red>13</font> 30 <br />
39 18 <font color=red>&nbsp;5</font> &nbsp;4 <font color=red>&nbsp;3</font> 12 29 <br />
40 19 &nbsp;6 &nbsp;1 &nbsp;2 11 28 <br />
41 20 <font color=red>&nbsp;7</font> &nbsp;8 &nbsp;9 10 27 <br />
42 21 22 23 24 25 26 <br />
<font color=red>43</font> 44 45 46 47 48 49
</center>

It is interesting to note that the odd squares lie along the bottom right diagonal, but what is more interesting is that $8$ out of the $13$ numbers lying along both diagonals are prime; that is, a ratio of $\dfrac{8}{13} \approx 62\%$.

If one complete new layer is wrapped around the spiral above, a square spiral with side length $9$ will be formed. If this process is continued, what is the side length of the square spiral for which the ratio of primes along both diagonals first falls below $10\%$?

## 解决方案

这个矩阵的四个角的元素的通项公式分别是：$4n^2-10n+7,4(n-1)^2+1,4n^2-6n+3,(2n-1)^2$，其中$n\ge 1$，用的是第28题的结论。

因此，这份代码将通过公式枚举出一个个质数，然后单独进行判断即可。

## 代码

```py
from tools import is_prime
from itertools import count

r = 0.1
c0 = 0
c1 = 1
for i in count(2, 1):
    for x in [4 * i * i - 10 * i + 7, 4 * (i - 1) * (i - 1) + 1, 4 * i * i - 6 * i + 3, (2 * i - 1) ** 2]:
        c1 += 1
        if is_prime(x):
            c0 += 1
    if c0 / c1 < r:
        ans = i * 2 - 1
        break
print(ans)

```
