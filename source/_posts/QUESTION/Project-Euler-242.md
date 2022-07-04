---
title: Project Euler 242
tags:
  - Project Euler
  - 卢卡斯定理
mathjax: true
date: 2022-07-04 18:02:33
---

<escape><!-- more --></escape>

# Project Euler 242

## 题目

### Odd Triplets

Given the set $\{1,2,\dots,n\}$, we define $f(n,k)$ as the number of its $k$-element subsets with an odd sum of elements. For example, $f(5,3)=4$, since the set $\{1,2,3,4,5\}$ has four $3$-element subsets having an odd sum of elements, i.e.: $\{1,2,4\}, \{1,3,5\}, \{2,3,4\}$ and $\{2,4,5\}$.

When all three values $n, k$ and $f(n,k)$ are odd, we say that they make an *odd-triplet* $[n,k,f(n,k)]$.
There are exactly five odd-triplets with $n\le10$, namely:$[1,1,f(1,1)=1], [5,1,f(5,1)=3], [5,5,f(5,5)=1], [9,1,f(9,1)=5]$ and $[9,9,f(9,9)=1]$.

How many odd-triplets are there with $n\le10^{12}$?

## 卢卡斯定理

[卢卡斯定理](https://en.wikipedia.org/wiki/Lucas%27s_theorem)：如果$p$是一个质数，那么计算组合数$C_n^m\% p$时可用以下公式。

$$C_n^m \equiv C_{n\%p}^{m\%p} \cdot C_{\lfloor\frac{n}{p}\rfloor}^{\lfloor\frac{m}{p}\rfloor}( \mod p)$$

其中，在计算过程中，如果发生了$m>n$，那么$C_n^m\%p=0$。

可以看成是假设有两个等长的$p$进制数（可以有前导$0$）：$a=a_{k-1}\dots a_2a_1a_0,b= b_{k-1}\dots b_2b_1b_0$。那么

$$C_a^b\equiv  C_{a_{k-1}}^{b_{k-1}}\dots C_{a_2}^{b_2}C_{a_1}^{b_1}C_{a_0}^{b_0}(\mod p) $$

## 解决方案

令$N=10^{12}$。将$f(i,j)$的所有奇数行和奇数列打印出来后，发现以下现象：

1. 如果$i,j$**其中一个**是形如$4k+3$的数，那么$f(i,j)$为偶数。这部分我们不需要考虑。
2. 如果$i,j$**都**是形如$4k+1$的数，那么$f(4k_0+1,4k_1+1)$的奇偶性将和$C_{k_0}^{k_1}$相同。

那么，这个问题就转化成了如下表述：在杨辉三角的前$\lfloor\dfrac{N+3}{4}\rfloor$行中，有多少个数是奇数？

这个问题的解决方式和148题完全相同，此处不再详述具体算法。

接下来主要详述为什么这些现象是成立的。

令$n=2a+1,m=2b+1$，那么不难发现，集合有$a$个偶数，$a+1$个奇数。为了保证选择的子集和是一个奇数，因此选择的$2b+1$个数中，必须有偶数个偶数。

那么，就可以写出：

$$f(n,m)=\sum_{ k=\lceil\frac{m-a-1}{2}\rceil}^{\lfloor\frac{a}{2}\rfloor} C_a^{2k}\cdot C_{a+1}^{m-2k}$$

发现$m-2k$必定为奇数，如果$a+1$是偶数，那么根据卢卡斯定理，$C_{a+1}^{m-2k}$必定是一个偶数。最终，$f(n,m)$为偶数。

因此$a$必定为偶数，令$a=2c$，那么$n=4c+1$。

代入$m=2b+1$，那么$f(n,m)$就可以重写成：

$$f(n,m)=\sum_{ k=\lceil\frac{m-2c-1}{2}\rceil}^{\lfloor\frac{a}{2}\rfloor} C_{2c}^{2k}\cdot C_{2c+1}^{2b-2k+1}=\sum_{ k=\lceil\frac{m-2c-1}{2}\rceil}^{\lfloor\frac{a}{2}\rfloor} C_{2c}^{2k}\cdot C_{2c+1}^{2(b-k)+1}$$

那么根据卢卡斯定理，可以写出：

$$f(n,m)\equiv \sum_{k} C_{c}^{k}\cdot C_{c}^{b-k} (\mod 2)$$

如果$b$是奇数，那么就可以写成：

$$f(n,m)\equiv 2\sum_{k< \frac{b}{2}} C_{c}^{k}\cdot C_{c}^{b-k} (\mod 2)$$

因为当$k>\dfrac{b}{2}$，求和式仍然是相同的。从式子中可以看出，此时$f(n,m)$是偶数。

因此$b$必须是偶数，令$b=2d$，那么$m=4d+1$，并且$f(n,m)$可以写成：

$$f(n,m)\equiv (C_c^d)^2+2\sum_{k<d} C_{c}^k\cdot C_c^{2d-k}\equiv C_c^d(\mod 2)$$

因此这种现象得证。由于$n=4c+1$，最终将问题转化成了求杨辉三角上前$\lfloor\dfrac{N+3}{4}\rfloor$行元素中奇数的个数。

## 代码

```py
N, p = 10 ** 12, 2


def fun(n: int):
    return n * (n + 1) // 2


N = (N + 3) // 4
ls = []
while N:
    ls.append(N % p)
    N //= p

ans, mul = 0, 1
for k in range(len(ls) - 1, -1, -1):
    ans += mul * (fun(p) ** k) * fun(ls[k])
    mul *= (ls[k] + 1)
print(ans)

```
