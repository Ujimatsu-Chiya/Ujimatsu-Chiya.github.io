---
title: Project Euler 776
category:
  - Project Euler
tags:
  - 动态规划
mathjax: true
date: 2022-07-27 23:49:26
---

<escape><!-- more --></escape>

# Project Euler 776

## 题目

### Digit Sum Division

For a positive integer $n$, $d(n)$ is defined to be the sum of the digits of $n$. For example, $d(12345)=15$.

Let $\displaystyle F(N)=\sum_{n=1}^N \frac n{d(n)}$.

You are given $F(10)=19$, $F(123)\approx 1.187764610390e3$ and $F(12345)\approx 4.855801996238e6$.

Find $F(1234567890123456789)$. Write your answer in scientific notation rounded to twelve significant digits after the decimal point. Use a lowercase e to separate the mantissa and the exponent.

## 解决方案

不难发现，可以将$F$进行改写：

$$F(N)=\sum_{n=1}^{N}\dfrac{n}{d(n)}=\sum_{k=1}^{+\infty}\dfrac{1}{k}\cdot(\sum_{n\le N,d(n)=k}n)$$

改写后，相当于将$1\sim N$以内的所有数按照数位和分类好，再将它们求和即可，考虑使用动态规划的方法进行。

令$N=1234567890123456789$。考虑将$N$写成一个长度为$l$的十进制字符串$N=d_1d_2d_3\dots d_l$。

由于$N$很小，因此总数位和不会很大。

令**中间**状态$c_1(i,j)(1\le i\le l,0\le j\le 9i)$分别表示如下含义：有多少个$i$位**有前导0**的数，其数位和为$j$，并**等于**由字符串$d_1d_2\dots d_i$表示的数。令状态$s_1(i,j)$表示$c_1(i,j)$中的所有数之和。

不难发现，如果$j=\sum_{k=1}^n d_i$，那么$c_1(i,j)=1$，$s_1(i,j)$的值则为$d_1d_2\dots d_i$这一个字符串的十进制数；否则$c_1(i,j)=s_1(i,j)=0$。

函数$c_1$和$s_1$的意义在于规定了答案严格在界限上的情况。而接下来定义的状态$c_0,s_0$则是严格不在界限上的情况。

令状态$c_0(i,j)$表示有多少个$i$位**有前导0**的数，其数位和为$j$，并**严格小于**由字符串$d_1d_2\dots d_i$表示的数。令状态$s_0(i,j)$表示$c_0(i,j)$中的所有数之和。

那么可以先写出$c_0$的状态转移方程：

$$
c_0(i,j)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=1\wedge j<d_1 \\
  &0 & & \mathrm{else if\quad} i=1 \\
  &\sum_{k=0}^{\min(9,n)} c_0(i-1,j-k)+\sum_{k=0}^{\min(9,n,d_i-1)} c_1(i-1,j-k) & & \mathrm{else}
\end{aligned}\right.
$$

方程最后一行的第一个求和项说明，如果之前的状态已经是严格小于$d_1d_2\dots d_{i-1}$的数，那么接下来无论拼接哪一个，都是严格小于的；对于第二个求和项而言，如果之前取的值都是严格等于的，那么接下来最多只能取到$d_{i-1}$。

那么基于$c_0$的思想，同样不难写出$s_0$的状态转移方程：

$$
s_0(i,j)=
\left \{\begin{aligned}
  &j  & & \mathrm{if\quad} i=1\wedge j<d_1 \\
  &0 & & \mathrm{else if\quad} i=1 \\
  &\sum_{k=0}^{\min(9,n)} (10\cdot s_0(i-1,j-k)+ k\cdot c_0(i-1,j-k))+\\
  &\sum_{k=0}^{\min(9,n,d_i-1)} (10\cdot s_1(i-1,j-k)+ k\cdot c_1(i-1,j-k)) & & \mathrm{else}
\end{aligned}\right.
$$

计算完成后，那么就可以计算$F(N)$：

$$F(N)=\sum_{k=1}^{9l}\dfrac{s_0(l,k)+s_1(l,k)}{k}$$

## 代码

```py
N = 1234567890123456789
d = list(map(int, list(str(N))))
l = len(d)
c = [[[0, 0] for _ in range((l + 1) * 9)] for _ in range(l)]
s = [[[0, 0] for _ in range((l + 1) * 9)] for _ in range(l)]
c[0][d[0]][1] = 1
s[0][d[0]][1] = d[0]
for j in range(d[0]):
    c[0][j][0] = 1
    s[0][j][0] = j
ds = d[0]
for i in range(1, l):
    ds += d[i]
    c[i][ds][1] = 1
    s[i][ds][1] = s[i - 1][ds - d[i]][1] * 10 + d[i]
    for j in range(l * 9):
        for k in range(min(j, 9) + 1):
            if k < d[i]:
                c[i][j][0] += c[i - 1][j - k][1]
                s[i][j][0] += s[i - 1][j - k][1] * 10 + c[i - 1][j - k][1] * k
            c[i][j][0] += c[i - 1][j - k][0]
            s[i][j][0] += s[i - 1][j - k][0] * 10 + c[i - 1][j - k][0] * k

ans = 0
for i in range(1, l * 9):
    ans += sum(s[-1][i]) / i
ans = "{:.12e}".format(ans).replace("e+", "e").replace("e0", "e")
print(ans)

```
