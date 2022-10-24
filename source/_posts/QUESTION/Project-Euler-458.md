---
title: Project Euler 458
category:
  - Project Euler
tags:
  - 动态规划
  - 矩阵快速幂
mathjax: true
date: 2022-06-08 22:37:32
---

<escape><!-- more --></escape>

# Project Euler 458

## 题目

### Permutations of Project

Consider the alphabet $A$ made out of the letters of the word "project": $A=\{c,e,j,o,p,r,t\}$.

Let $T(n)$ be the number of strings of length $n$ consisting of letters from $A$ that do not have a substring that is one of the $5040$ permutations of “project”.

$T(7)=7^7-7!=818503$.

Find $T(10^{12})$. Give the last $9$ digits of your answer.

## 解决方案

使用动态规划的思想做，使用矩阵快速幂进行优化。

令$N=10^{12},M=7$。设$f(i,j)(1\le i \le N,1\le j< M,j\le i)$为以下字符串的个数：长度为$i$，最后$j$个字符两两不同，但是最后$j+1$个字符却不是两两不同的。

那么以矩阵的形式写出状态转移方程：

$$
\begin{bmatrix}
1 & 1 & 1 & 1 & 1 & 1\\
6 & 1 & 1 & 1 & 1 & 1\\
0 & 5 & 1 & 1 & 1 & 1\\
0 & 0 & 4 & 1 & 1 & 1\\
0 & 0 & 0 & 3 & 1 & 1\\
0 & 0 & 0 & 0 & 2 & 1
\end{bmatrix}
\begin{bmatrix}
f(i-1,1)\\
f(i-1,2)\\
f(i-1,3)\\
f(i-1,4)\\
f(i-1,5)\\
f(i-1,6)
\end{bmatrix}
=
\begin{bmatrix}
f(i,1)\\
f(i,2)\\
f(i,3)\\
f(i,4)\\
f(i,5)\\
f(i,6)
\end{bmatrix}
$$

其中$f(1,1)=7,f(1,2)=f(1,3)=\dots=f(1,6)=0$。

对于状态$f(i,j)$，最后$j$个字符不同，那么可以随意新添加一个字符变成状态$f(i+1,j+1)$，有$m-j$种添加方式。或者是添加第$j$个字符中的倒数第$k$个，转换成状态$f(i+1,k)$（如以下例子）：

一个字符串~~03~~4523，添加一个5，变成~~0345~~235，也就是从$f(i,4)$转移到了$f(i+1,3)$；如果是添加一个2，那么变成~~03452~~32，转换成了状态$f(i+1,2)$；如果是添加一个6（同0和1），那么变成~~03~~45236，转换成状态$f(i+1,4)$。

最终，直接使用矩阵快速幂进行处理即可，答案为$\sum_{j=1}^{m-1}f(n,j)$。

## 代码

```py
n = 10 ** 12
m = 7
mod = 10 ** 9


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


a = [[m] + [0 for i in range(m - 2)]]
b = [[0 for _ in range(m - 1)] for _ in range(m - 1)]
for i in range(m - 2):
    b[i][i + 1] = m - i - 1
for i in range(m - 1):
    for j in range(i + 1):
        b[i][j] = 1
n -= 1
while n:
    if n & 1:
        a = mul(a, b)
    b = mul(b, b)
    n >>= 1
ans = sum(a[0]) % mod
print(ans)

```
