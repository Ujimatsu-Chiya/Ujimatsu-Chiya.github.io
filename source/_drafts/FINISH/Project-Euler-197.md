---
title: Project Euler 197
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 197
## 题目
### Investigating the behaviour of a recursively defined sequence

Given is the function $f(x) = \lfloor 2^{30.403243784}-x^2\rfloor \times 10^{-9}$ ( $\lfloor \quad \rfloor$  is the floor-function), the sequence $u_n$ is defined by $u_0 = -1$ and $u_{n+1} = f(u_n)$.

Find $u_n + u_{n+1}$ for $n = 10^{12}$.

Give your answer with $9$ digits after the decimal point.


## 解决方案

将序列打印出多项后发现，到了某一个下标之后，数列的值是两个数反复交替出现。因此美剧量为常数，直接模拟。

## 代码


```py
N = 10 ** 12
M = min(N, 600)


def f(x: float):
    return int(2 ** (30.403243784 - x * x)) * 1e-9


a = [-1]
for i in range(M):
    a.append(f(a[-1]))
ans = a[M] + a[M - 1]
print(ans)

```