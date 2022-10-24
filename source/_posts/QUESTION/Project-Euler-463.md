---
title: Project Euler 463
tags:
  - OEIS
category:
  - Project Euler
mathjax: true
date: 2022-08-21 23:51:02
---

<escape><!-- more --></escape>

# Project Euler 463

## 题目

### A weird recurrence relation

The function $f$ is defined for all positive integers as follows:

- $f(1)=1$
- $f(3)=3$
- $f(2n)=f(n)$
- $f(4n + 1)=2f(2n + 1) - f(n)$
- $f(4n + 3)=3f(2n + 1) - 2f(n)$

The function $S(n)$ is defined as $\sum_{i=1}^{n}f(i)$.

$S(8)=22$ and $S(100)=3604$.

Find $S(3^{37})$. Give the last $9$ digits of your answer.

## 解决方案

暴力枚举出$f$的前几项，在OEIS中查询得到结果为[A030101](https://oeis.org/A030101)。

标题已经介绍了$f(n)$的含义：将$n$的二进制的所有比特进行逆序后得到的值。

因此，计算$S(n)$时，分块计算：$[2^0,2^1),[2^1,2^2),\dots,[2^i,2^{i+1})$中的和。不难发现：

$$\sum_{j=2^i}^{2^{i+1}-1}f(j)=2^i+\dfrac{2^i\cdot (0+2^i-1)}{2} \cdot 2=2^{2i}$$

对于满足$2^i\le n <2^{i+1}-1$的这个区间，我们采用另一种计算方式。

将$n$写成一个$k$位二进制数$n=n_0n_1n_2\dots n_{k-1}$，从高到低位遍历位数，如果$n_i=1$，那么对于任意$m$满足$m_0=n_0,m_1=n_1,\dots,m_{i-1}=n_{i-1}$，如果$m_i=0$，那么说明无论$m_{i+1},m_{i+2},\dots,m_k$怎么取，$m<n$ 均成立。因为最后面这一部分是自由选择的，我们将这一部分合并在一起算。

如以下例子，`'.'`上的数无论怎么取，都比$n$小：

```
n = 1 0 1 0 1 0 0 0 1 0 1 0
m = 1 0 0 . . . . . . . . .
```

因此，这一部分的和为

$$\dfrac{2^{k-i-1}\cdot (2^{k-i-1}-1)}{2} \cdot 2^{i+1} + g_n(i)\cdot 2^{k-i-1}$$

其中$g_n(i)$表示二进制数$n_{i-1}n_{i-2}\dots n_1n_0.$

按照上面的计算方法，枚举求和即可。注意需要跳过最高位，也就是$i=0$的情况。

## 代码

```py
N = 3 ** 37
mod = 10 ** 9
N += 1
s = 1
ans = 0
while s * 2 <= N:
    ans += (s - 1) * s + s
    s <<= 1
ls = list(map(int, list(bin(N)[2:])))
st = 0
for i in range(len(ls)):
    if i > 0 and ls[i]:
        k = 1 << (len(ls) - i - 1)
        w = (k - 1) * k
        ans += st * k + (w << i)
    st |= ls[i] << i
ans %= mod
print(ans)

```
