---
title: Project Euler 248
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 248
## 题目
### Numbers for which Euler’s totient function equals 13!


The first number n for which $\varphi(n)=13!$ is $6227180929$.

Find the $150,000^{\text{th}}$ such number.


## 解决方案

令$M=13!$。如果$\varphi(n)=M$，那么$n$的所有质因数$p$的欧拉函数$\varphi(p)=p-1$，都有$p-1|M$。

那么，先求出$M$的所有因数$d$，再将所有是质数的$d+1$存入数组$pr$中。

最终，$n$一定是由数组$pr$的一些质因子相乘而得。

考虑通过深度优先搜索，枚举出所有$\varphi(n)=M$的$n$值。**从大到小**枚举所有质因数并逐一尝试，这样做可以有效减少枚举量。

## 代码


```py
from tools import fac, is_prime, divisors

N = 13
Q = 150000
M = fac(N)
pr = [x + 1 for x in divisors(M) if is_prime(x + 1)][::-1]
ls = []


def dfs(f, n, rest):
    if rest == 1:
        ls.append(n)
    for i in range(f, len(pr)):
        p = pr[i]
        if rest % (p - 1) == 0:
            dfs(i + 1, n * p, rest // (p - 1))
            t_n, t_rest = n * p, rest // (p - 1)
            while t_rest % p == 0:
                t_rest //= p
                t_n *= p
                dfs(i + 1, t_n, t_rest)


dfs(0, 1, M)
ls.sort()
ans = ls[Q - 1]
print(ans)
# 16s~17s

```