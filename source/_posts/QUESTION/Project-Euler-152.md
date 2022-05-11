---
title: Project Euler 152
tags:
  - Project Euler
  - meet-in-the-middle
mathjax: true
date: 2022-05-11 19:27:44
---

<escape><!-- more --></escape>

# Project Euler 152

## 题目

### Writing 1/2 as a sum of inverse squares

There are several ways to write the number $\dfrac{1}{2}$ as a sum of inverse squares using *distinct* integers.

For instance, the numbers $\{2,3,4,5,7,12,15,20,28,35\}$ can be used:
$$\dfrac{1}{2} = \dfrac{1}{2^2} + \dfrac{1}{3^2} + \dfrac{1}{4^2} + \dfrac{1}{5^2}+
\dfrac{1}{7^2} + \dfrac{1}{12^2} + \dfrac{1}{15^2} + \dfrac{1}{20^2} +
\dfrac{1}{28^2} + \dfrac{1}{35^2}$$

In fact, only using integers between $2$ and $45$ inclusive, there are exactly three ways to do it, the remaining two being: $\{2,3,4,6,7,9,10,20,28,35,36,45\}$ and $\{2,3,4,6,7,9,12,15,28,30,35,36,45\}$.

How many ways are there to write the number $\dfrac{1}{2}$ as a sum of inverse squares using distinct integers between $2$ and $80$ inclusive?

## 解决方案

本解决方案参考了Thread中的一些内容。

为减少枚举量，进行以下排除：

1. 考虑所有质数$p$，令$q=p^r$，其中$r$是使$p^r$不超过$N=80$的最大值。

在这种情况下，考虑所有满足$kq\le N$的分数$\dfrac{1}{q^2},\dfrac{1}{(2q)^2},\dots,\dfrac{1}{(kq)^2}$

考虑计算$\dfrac{1}{(i_1q)^2}+\dfrac{1}{(i_2q)^2}+\dots+\dfrac{1}{(i_mq)^2}$，其中$i_j<p$，不同的$i_j$之间两两不同。

那么有$\dfrac{1}{q^2}(\dfrac{1}{i_1^2}+\dfrac{1}{i_2^2}+\dots+\dfrac{1}{i_m^2})$

如果在计算分数和的过程中，分母混进了一个非$2$的质数$p$，那么在以后求和的过程中必须消除分母$p$。因此$\sum_{j=1}^m i_j^{-2}$在模$q^2$上与$0$同余。

- 对于大于$\dfrac{N}{2}$的质数而言，只有一个$m=1,i_1=1$，也就是$\{1\}$，不可能存在一个非空集合使得其子集和为$0$。故排除这一类情况。

- 对于质数$p=11$，那么$i_j\in[1,7]$，也就是说，$i_j^{-2}\% p^2 \in\{1, 91, 27, 53, 92, 37, 42\}$，容易经过验证，没有一个非空子集的和为$p^2$，故排除$11$的所有倍数。

- 对于质数$p=13$，那么$i_j\in[1,6]$，也就是说，$i_j^{-2}\% p^2 \in\{1, 127, 94, 74, 142, 108\}$，容易经过验证，只有$1+94+74=169$才是$p^2$的倍数，因此除了$13,39,52$，其它都可以排除。而且，这三个数只有一起用才能消除掉分母$13$。经计算得$\dfrac{1}{13^2}+\dfrac{1}{39^2}+\dfrac{1}{52^2}=\dfrac{1}{12^2}$，所以可以在候选集中多添加一个$12$。然后忽略这$3$个数。

可以用类似的方法，排除掉以下这些数：$\{17,34,51,68,19,38,57,76,23,46,69,27,54,29,58,49,64,...\}$

更进一步，如果$q=p^r$中的$r$不一定是满足最大值，上述$i_j$也只是满足$\gcd(i_j,q)=1$，那么用类似的方法，可以将$\{16,32,48,80\}$排除。

2. 根据上面的排除结果，剩下的数中，$\dfrac{1}{2^2},\dfrac{1}{3^2}$一定是在集合中的，因为缺少了这两个数之一，剩下的分数的和小于$\dfrac{1}{2}$。因此不需要对这两个数枚举，只要在最终和值$\dfrac{1}{2}$中减去即可。

按照上面的方法，最终只需要枚举$27$个数的组合情况。

这里则使用meet-in-the-middle思想：先将分数分成尽量相同大小的两部分，然后子集枚举第一部分，并按子集和$s$将结果存储起来，然后子集枚举第二部分，求出$s'$后，在第一部分的枚举结果中查找有没有那缺失的$s$，使得$s+s'$是原来的问题的解。如果有，那就找到了解。

## 代码

```py
from fractions import Fraction

ls = [4, 5, 6, 7, 8, 9, 10, 12, 12, 14, 15, 18, 20, 21, 24, 28, 30, 35, 36, 40, 42, 45, 56, 60, 63, 70, 72]

ans = 0
n = len(ls)
the_sum = Fraction(1, 2) - Fraction(1, 4) - Fraction(1, 9)
l, r = ls[:n // 2], ls[n // 2:]
mp = {}
for i in range(1 << len(l)):
    s = Fraction(0)
    for j in range(len(l)):
        if i >> j & 1:
            s += Fraction(1, l[j] * l[j])
    if s <= the_sum:
        if s not in mp.keys():
            mp[s] = 0
        mp[s] += 1
for i in range(1 << len(r)):
    s = Fraction(0)
    for j in range(len(r)):
        if i >> j & 1:
            s += Fraction(1, r[j] * r[j])
    t = the_sum - s
    if t in mp.keys():
        ans += mp[t]
print(ans)

```
