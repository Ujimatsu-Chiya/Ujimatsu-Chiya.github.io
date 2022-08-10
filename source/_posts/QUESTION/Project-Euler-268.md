---
title: Project Euler 268
category:
  - Project Euler
tags:
  - 容斥原理
mathjax: true
date: 2022-07-04 18:02:16
---

<escape><!-- more --></escape>

# Project Euler 268

## 题目

### Counting numbers with at least four distinct prime factors less than 100

It can be verified that there are $23$ positive integers less than $1000$ that are divisible by at least four distinct primes less than $100$.

Find how many positive integers less than $10^{16}$ are divisible by at least four distinct primes less than $100$.

## 解决方案

令$M=23,N=10^{16},K=4,p_j$为这$M$个质数之一。

那么根据容斥原理，答案为：

$$\sum_{i=K}^M (-1)^{i-K}\cdot \dbinom{i-1}{K-1}\cdot \sum_{p_1<p_2<\dots<p_i}\dfrac{N}{\prod_{j=1}^ip_j}$$

其中前两项是容斥原理的系数，第一个则是将至少$K$个的添加，然后将重复算的$K+1$个减去，再将被重复减去的$K+2$个的补充回来……；第二个表示，这个大小为$i$的集合被之前重复的计算次数。

第三项则是求$N$以内有多少个数同时具有$p_1,p_2,\dots,p_j$这$j$个质因子，一共有$\dfrac{N}{\prod_{j=1}^ip_j}$个。

## 代码

```py
from tools import get_prime, C

N = 10 ** 16
M = 100
K = 4
N -= 1
pr = get_prime(M - 1)
s = [0 for i in range(len(pr) + 1)]


def dfs(f: int, n: int, v: int):
    if f == len(pr) or n * pr[f] > N:
        s[v] += N // n
        return
    dfs(f + 1, n, v)
    dfs(f + 1, n * pr[f], v + 1)


dfs(0, 1, 0)
ans = 0
flag = True
for i in range(K, len(s)):
    if flag:
        ans += s[i] * C(i - 1, K - 1)
    else:
        ans -= s[i] * C(i - 1, K - 1)
    flag = not flag
print(ans)

```
