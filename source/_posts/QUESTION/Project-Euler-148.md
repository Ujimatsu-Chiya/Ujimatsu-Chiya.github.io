---
title: Project Euler 148
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-11 19:27:36
---

<escape><!-- more --></escape>

# Project Euler 148

## 题目

### Exploring Pascal’s triangle

We can easily verify that none of the entries in the first seven rows of Pascal’s triangle are divisible by $7$:

||||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|-|-|
|||||||1|||||||
||||||1||1||||||
|||||1||2||1|||||
||||1||3||3||1||||
|||1||4||6||4||1|||
||1||5||10||10||5||1||
|1||6||15||20||15||6||1|

However, if we check the first one hundred rows, we will find that only $2361$ of the $5050$ entries are not divisible by $7$.

Find the number of entries which are not divisible by $7$ in the first one billion ($10^9$) rows of Pascal’s triangle.

## 卢卡斯定理

[卢卡斯定理](https://en.wikipedia.org/wiki/Lucas%27s_theorem)：如果$p$是一个质数，那么计算组合数$C_n^m\% p$时可用以下公式。

$$C_n^m \equiv C_{n\%p}^{m\%p} \cdot C_{\lfloor\frac{n}{p}\rfloor}^{\lfloor\frac{m}{p}\rfloor}( \mod p)$$

其中，在计算过程中，如果发生了$m>n$，那么$C_n^m\%p=0$。

可以看成是假设有两个等长的$p$进制数（可以有前导$0$）：$a=a_{k-1}\dots a_2a_1a_0,b= b_{k-1}\dots b_2b_1b_0$。那么

$$C_a^b\equiv  C_{a_{k-1}}^{b_{k-1}}\dots C_{a_2}^{b_2}C_{a_1}^{b_1}C_{a_0}^{b_0}(\mod p) $$

## 解决方案

根据卢卡斯定理，上面的问题可以转化成另一种形式。有多少对$(i,j)(0\leq j \le i <n )$，满足以下条件：

将$i$和$j$写成两个长度为$k$的$p$进制数：$i=i_{k-1}\dots i_2i_1i_0,j=j_{k-1}\dots j_2j_1j_0$。那么$\forall q:0\le q<k ,j_q\le i_q $.

根据卢卡斯定理的描述，如果有一个$j_q>i_q$，那么整个式子模$p$的值为$0$，也就是能被$p$整除。

设$p$进制数$n=n_{k-1}\dots n_2n_1n_0$，那么对于每一个$q\in[0,k-1]$，如果$n_{k-1}=i_{k-1},n_{k-2}=i_{k-2},\dots,i_{q+1}=n_{q+1},i_q<n_q$，可以将这一些数位的下标划分成独立的三个部分：

1. $q-1,q-2,\dots 0$这一部分。 $i_{q-1},i_{q-2},\dots,i_0$都可以随便填$0,1,\dots,p-1$这$p$个数，而每个$j_{k-1}\le i_{k-1},j_{k-2}\le i_{k-2},\dots,j_0\le i_0$都要得到保证，因此后面这些数一共有$(\dfrac{p(p+1)}{2})^{k+1}$种填法。

2. $q$自己的一部分。$0\le j_q\le i_q<n_q$，满足这个条件的$(j_q,i_q)$对数为$\dfrac{n_q(n_q+1)}{2}$。

3. $k-1,k-2,\dots,q+1$这一部分。这一部分的$n$和$i$的数位相等，$i$的部分是固定的，$j$是变动的，都有$0\le j_m\le i_m=n_m$。因此每个独立数位都有$n_m+1$种填法。

三种情况独立考虑，因此最终答案为$$\sum_{q=0}^{k-1} (\dfrac{p(p+1)}{2})^{k+1}\cdot \dfrac{n_q(n_q+1)}{2}\cdot \prod_{m=q+1}^{k-1}n_m$$

## 代码

```py
N, p = 10 ** 9, 7


def fun(n: int):
    return n * (n + 1) // 2


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
