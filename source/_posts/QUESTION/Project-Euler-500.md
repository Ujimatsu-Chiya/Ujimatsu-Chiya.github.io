---
title: Project Euler 500
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-08 22:37:41
---

<escape><!-- more --></escape>

# Project Euler 500

## 题目

### Problem 500

The number of divisors of $120$ is $16$.

In fact $120$ is the smallest number having $16$ divisors.

Find the smallest number with $2^{500500}$ divisors.

Give your answer modulo $500500507$.

## 解决方案

注意到，所求的数的除数是一个二次幂（$2^{N},N=500500$）,那么所求的这个数一定是形如这种形式：

$$2^{2^{e_1}-1}\times3^{2^{e_2}-1}\times 5^{2^{e_3}-1}\times \dots$$

如果要令一个数$n$的因子数翻倍，观察$n$的因数个数公式$\prod (e_i+1)$，有以下两个操作办法：

- 为$n$乘上一个$n$中还未存在的质因数，这相当于添加了一个新的项$(1+1)$。
- $n$的分解质因数中，假设其中一项为$p_i^{e_i}$，那么就为$n$乘上$p_i^{e_i+1}$，这相当于把项$(e_i+1)$变成了$(2e_i+2)$。另外，如果当前对应质因子$p_i$的一项是$x$，那么下一次待添加的就是$x^2$。

因此，使用优先队列维护这些等待被$n$相乘的数，找出最小的一个为$n$乘上即可，过程迭代$N$次。

## 代码

```py
from tools import get_prime
from queue import PriorityQueue

M = 500500
mod = 500500507
pr = get_prime(M * int(len(bin(M)) - 2) + 14)
N = M * int(len(bin(M)) - 2)
q = PriorityQueue()
for i in range(M):
    q.put(pr[i])
ans = 1
for i in range(M):
    x = q.get()
    ans = ans * x % mod
    q.put(x * x)
print(ans)

```
