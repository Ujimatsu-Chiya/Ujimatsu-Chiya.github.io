---
title: Project Euler 69
tags:
  - Project Euler
mathjax: true
date: 2022-04-30 10:32:28
---

<escape><!-- more --></escape>

# Project Euler 69

## 题目

### Totient maximum

Euler’s Totient function, $\varphi(n)$ [sometimes called the phi function], is used to determine the number of numbers less than $n$ which are relatively prime to $n$. For example, as $1, 2, 4, 5, 7,$ and $8$, are all less than nine and relatively prime to nine, $\varphi(9)=6$.

|$n$|Relatively Prime|$\varphi(n)$|$n/\varphi(n)$|
|-|-|-|-|
|$2$|$1$|$1$|$2$|
|$3$|$1,2$|$2$|$1.5$|
|$4$|$1,3$|$2$|$2$|
|$5$|$1,2,3,4$|$4$|$1.25$|
|$6$|$1,5$|$2$|$3$|
|$7$|$1,2,3,4,5,6$|$6$|$1.1666\dots$|
|$8$|$1,3,5,7$|$4$|$2$|
|$9$|$1,2,4,5,7,8$|$6$|$1.5$|
|$10$|$1,3,7,9$|$4$|$2.5$|

It can be seen that $n=6$ produces a maximum $n/\varphi(n)$ for $n \leq 10$.

Find the value of $n \leq 1,000,000$ for which $n/\varphi(n)$ is a maximum.

## [欧拉函数](https://mathworld.wolfram.com/TotientFunction.html)

如果一个正整数$n$分解后成为：
$$n=\prod p_i^{e_i}$$
那么，欧拉函数值为：
$$\varphi(n)=n\prod(1-\dfrac{1}{p_i})$$

## 解决方案

欧拉筛不仅可以用来筛选素数，还可以以$O(\log n)$的时间复杂度计算积性函数的值。

具体过程是，筛选出一个质数$p$后，遍历其所有倍数$i=kp$时，可以按照上式，对欧拉函数数组phi尽心如此操作：$phi[i]:=phi[i] / p * (p-1)$。

一开始时，欧拉函数值都是默认为自身。

因此，本题就只需要计算出所有欧拉函数值，然后找到$n/\varphi(n)$最大的$n$即可。

## 代码

```py
N = 1000000
phi = [i for i in range(N + 1)]

val = 0
ans = 0
for i in range(2, N + 1):
    if i == phi[i]:
        for j in range(i, N + 1, i):
            phi[j] //= i
            phi[j] *= i - 1
    w = i / phi[i]
    if w > val:
        val = w
        ans = i
print(ans)

```
