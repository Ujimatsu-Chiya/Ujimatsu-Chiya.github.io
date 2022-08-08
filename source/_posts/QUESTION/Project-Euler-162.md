---
title: Project Euler 162
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-15 10:15:40
---

<escape><!-- more --></escape>

# Project Euler 162

## 题目

### Hexadecimal numbers

In  the hexadecimal number system numbers are represented using $16$ different digits:

$$0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F$$

The hexadecimal number $AF$ when written in the decimal number system equals $10\times 16+15=175$.

In the $3$-digit hexadecimal numbers $10A$, $1A0$, $A10$, and $A01$ the digits $0,1$ and $A$ are all present.

Like numbers written in base ten we write hexadecimal numbers without leading zeroes.

How many hexadecimal numbers containing at most sixteen hexadecimal digits exist with all of the digits $0,1$, and $A$ present at least once?

Give your answer as a hexadecimal number.

($A,B,C,D,E$ and $F$ in upper case, without any leading or trailing code that marks the number as hexadecimal and without leading zeroes , e.g. 1A3F and not: 1a3f and not 0x1a3f and not $1A3F and not #1A3F and not 0000001A3F)

## 解决方案

一道明显的数位动态规划。每次都可以在一个数后面添加16种位。

因此，令$N=16$，假设$f(i,j)(i\ge 1,0\le j\le3)$为$i$位十六进制数中，已经使用了$0,1,A$中的$j$个数位的数有多少个。那么可以列出如下状态转移方程：

$$
f(i,j)=
\left \{\begin{aligned}
  &2  & & \mathrm{if\quad} i=1\&j=1 \\
  &13 & & \mathrm{else if\quad} i=1\&j=0\\
  &13f(i-1,j) & & \mathrm{else if\quad} j=0\\
  &(13+j)f(i-1,j)+(4-j)f(i-1,j-1) & & \mathrm{else}
\end{aligned}\right.
$$

在最后一行有两个方法：要么在一个$i-1$使用并且已经用过的$j$种数位，有$(13+j)f(i-j,1)$种添加方法；要么添加一个要求使用却未使用的数位，有$(4-j)f(i-1,j-1)$种添加方法。

最终答案为$\sum_{i=1}^nf(i,3)$。

## 代码

```py
N = 16
f = [[0, 0, 0, 0] for i in range(N + 1)]
f[1][0] = 13
f[1][1] = 2
for i in range(2, N + 1):
    for j in range(4):
        f[i][j] = f[i - 1][j] * (13 + j) + (0 if j == 0 else (4 - j) * f[i - 1][j - 1])
ans = sum(f[i][3] for i in range(1, N + 1))
print("{:X}".format(ans))

```
