---
title: Project Euler 759
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:51:23
tags:
  - OEIS
  - 动态规划
---

<escape><!-- more --></escape>

# Project Euler 759

## 题目

### A squared recurrence relation

The function $f$ is defined for all positive integers as follows:

$$\begin{aligned}
f(1) &=  1\\
f(2n) &= 2f(n)\\
f(2n+1) &= 2n+1 + 2f(n)+\dfrac 1n f(n)
\end{aligned}$$

It can be proven that $f(n)$ is integer for all values of $n$.

The function $S(n)$ is defined as $S(n) = \displaystyle \sum_{i=1}^n f(i) ^2$.

For example, $S(10)=1530$ and $S(10^2)=4798445$.

Find $S(10^{16})$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

暴力枚举出$f$的前几项，在OEIS中查询得到结果为[A245788](https://oeis.org/A245788)。

令$b(n)$表示$n$的二进制表示中有多少个$1$，那么按照题意，$f(n)=n\cdot b(n)$。

将$S$进行改写：

$$S(n)=\sum_{i=1}^{\lfloor\log_2 (n+1)\rfloor} \left(i^2\cdot \sum_{\substack{m\le n,b(m)=i}} m^2\right)$$

也就是说，问题转化成枚举$i$，求$n$以内的所有数中，满足$b(m)=i$的所有$m^2$之和。

将$n$写成一个长度为$l$的二进制数字符串$d_1d_2\dots d_l$，也就是有$l=\lfloor\log_2 (n+1)\rfloor$。

令**中间**状态$c_1(i,j)(1\le i\le l,0\le j\le 9i)$分别表示如下含义：有多少个$i$位**有前导0**的数，其二进制有$j$个$1$，并**等于**由字符串$d_1d_2\dots d_i$表示的数。令状态$s_1(i,j)$表示$c_1(i,j)$中的所有数之和。令状态$t_1(i,j)$表示$c_1(i,j)$中的所有数的**平方和**。

不难发现，如果$j=\sum_{k=1}^i d_k$，那么$c_1(i,j)=1$，$s_1(i,j)$的值则为$d_1d_2\dots d_i$这一个字符串的二进制数，并且$t_1(i,j)=s_1(i,j)^2$；否则$c_1(i,j)=s_1(i,j)=t_1(i,j)=0$。

状态$c_1,s_1,t_1$的意义在于规定了答案严格在界限上的情况。而接下来定义的状态$c_0,s_0,t_0$则是严格不在界限上的情况。

令状态$c_0(i,j)$表示有多少个$i$位**有前导0**的数，其数位和为$j$，并**严格小于**由字符串$d_1d_2\dots d_i$表示的数。令状态$s_0(i,j)$表示$c_0(i,j)$中的所有数之和，$t_0(i,j)$表示$c_0(i,j)$。中的所有数的平方和。

那么可以先写出$c_0$的状态转移方程：

$$
c_0(i,j)=
\left \{\begin{aligned}
  &1 & & \text{if}\quad  j=0 \\
  &0 & & \text{else if}\quad  i=1 \\
  &c_0(i-1,j-1)+c_0(i-1,j)+[d_i=1]\cdot c_1(i-1,j) & & \text{else}
\end{aligned}\right.
$$

其中，$[]$表示示性函数，如果$[]$内的表达式为真，那么值为$1$，否则为$0$。方程的前两项，如果之前的状态已经是严格小于$d_1d_2\dots d_{i-1}$的数，那么接下来无论在后面拼接一个$0$还是一个$1$，都是严格小于的；对于第三项而言，如果之前取的值都是严格等于的，那么接下来如果$d_i=1$，那么可以拼接一个$0$，从而达到**严格**小于的情况。

根据上面的思想，不难写出$s_0(i,j)$和$t_0(i,j)$：

$$
s_0(i,j)=
\left \{\begin{aligned}
  &0 & & \text{if}\quad  i=1\lor j=0 \\
  &2\cdot s_0(i-1,j-1)+c_0(i-1,j-1)+2\cdot s_0(i-1,j)+\\
  & [d_i=1]\cdot 2\cdot s_1(i-1,j) & & \text{else}
\end{aligned}\right.
$$

$$
t_0(i,j)=
\left \{\begin{aligned}
  &0 & & \text{if}\quad  i=1\lor j=0 \\
  &4\cdot t_0(i-1,j-1)+4\cdot s_0(i-1,j-1)+c_0(i-1,j-1)+4\cdot t_0(i-1,j)+\\
  &[d_i=1]\cdot 2\cdot s_1(i-1,j) & & \text{else}
\end{aligned}\right.
$$

需要注意的是，对于$t_0$的状态转移方程最后一行的前三项，系数是$4,4,1$，来自于平方式$(2n+1)^2=4n^2+4n+1$。

计算完成后，得到最终答案为：

$$S(n)=\sum_{i=1}^{l} i^2\cdot (t_0(l,i)+t_1(l,i))$$

## 代码

```py
N = 10 ** 16
mod = 1000000007
d = list(map(int, list(bin(N)[2:])))
l = len(d)
c = [[[0, 0] for _ in range(l + 1)] for _ in range(l)]
s = [[[0, 0] for _ in range(l + 1)] for _ in range(l)]
t = [[[0, 0] for _ in range(l + 1)] for _ in range(l)]
c[0][1][1] = s[0][1][1] = t[0][1][1] = 1
c[0][0][0] = 1
cnt = 1
for i in range(1, l):
    cnt += d[i]
    c[i][cnt][1] = 1
    s[i][cnt][1] = s[i - 1][cnt - d[i]][1] * 2 + d[i]
    # 因为d[i]=0,1,d[i] ** 2 = d[i]
    t[i][cnt][1] = t[i - 1][cnt - d[i]][1] * 4 + s[i - 1][cnt - d[i]][1] * d[i] * 4 + d[i]
    c[i][0][0] = 1
    s[i][0][0] = t[i][0][0] = 0
    for j in range(1, l + 1):
        c[i][j][0] = c[i - 1][j - 1][0] + c[i - 1][j][0]
        s[i][j][0] = s[i - 1][j - 1][0] * 2 + c[i - 1][j - 1][0] + s[i - 1][j][0] * 2
        t[i][j][0] = t[i - 1][j - 1][0] * 4 + s[i - 1][j - 1][0] * 4 + c[i - 1][j - 1][0] + t[i - 1][j][0] * 4
        if d[i] == 1:
            c[i][j][0] += c[i - 1][j][1]
            s[i][j][0] += s[i - 1][j][1] * 2
            t[i][j][0] += t[i - 1][j][1] * 4

ans = 0
for i in range(l + 1):
    ans += sum(t[-1][i]) * i * i
ans %= mod
print(ans)

```
