---
title: Project Euler 241
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 241
## 题目
### Perfection Quotients


For a positive integer $n$, let $\sigma(n)$ be the sum of all divisors of $n$. For example, $\sigma(6) = 1 + 2 + 3 + 6 = 12$.

A perfect number, as you probably know, is a number with $\sigma(n) = 2n$.

Let us define the **perfection quotient** of a positive integer as $p(n) = \dfrac{\sigma(n)}{n}$.

Find the sum of all positive integers $n \le 10^{18}$ for which $p(n)$ has the form $k + \dfrac{1}{2}$, where $k$ is an integer.



## 解决方案



可以将$\dfrac{\sigma(n)}{n}=k+\dfrac{1}{2}$改写成：

$$\dfrac{(2k+1)\cdot n}{2\sigma(n)}=1$$


对于一个质数$q$，有$p(q^k)=\dfrac{q^{k+1}-1}{q-1}\cdot\dfrac{1}{q^k}$.

给定一个数$\dfrac{a}{b}=\dfrac{2k+1}{2}$，不停除上一些形如$p(q_i^{k_i})$的值（其中$q_i$是质数），那么这个数将会逐渐减少。如果恰好能减少到$1$，那么就找到了一个答案$\prod_i q_i^{k_i}$.如果在除的过程中发现这个数小于$1$了，那么就返回。

对于质数$q_i$的寻找方式：为了尽快消去分母$b$，考虑对$b$进行分解质因数，那么假设找到$b$的分解中最小的一项为$r^e$。那么就对$\dfrac{a}{b}$尝试除$p(r^e),p(r^{e+1}),p(r^{e+2}),\dots$往下继续进行搜索。

关于$k$的枚举，该[页面](https://en.wikipedia.org/wiki/Divisor_function)给出了$p(n)(n>3)$的上限：

$$\dfrac{\sigma(n)}{n}<e^{\gamma} \log\log n+\dfrac{0.6483}{\log\log n}$$

其中$\gamma$为欧拉常数，值约为$0.57721 56649$.因此，只需要保证$\dfrac{2k+1}{2}$在这个范围内即可。




## 代码

```py
from tools import gcd, factorization
from itertools import count
from math import exp, log

N = 10 ** 18
ans = 0
K = int((exp(0.577215664901532) * log(log(N)) + 0.6483 / log(log(N)))*2)


def dfs(n: int, fz: int, fm: int):
    if n * fz > N or gcd(n, fm) != 1 or fz < fm:
        return
    if fm == 1:
        if fz == 1:
            global ans
            ans += n
        return
    p = factorization(fm)[0][0]
    e = 1
    while fm % p ** (e + 1) == 0:
        e += 1
    for i in count(e, 1):
        nw = n * p ** i
        if nw > N:
            break
        new_fz = fz * p ** i
        new_fm = fm * (p ** (i + 1) - 1) // (p - 1)
        g = gcd(new_fz, new_fm)
        dfs(nw, new_fz // g, new_fm // g)


for i in range(3, K+1, 2):
    dfs(1, i, 2)
print(ans)

```