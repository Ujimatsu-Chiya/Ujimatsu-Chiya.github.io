---
title: Project Euler 175
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-17 22:21:16
---

<escape><!-- more --></escape>

# Project Euler 175

## 题目

### Fractions involving the number of different ways a number can be expressed as a sum of powers of 2

Define $f(0)=1$ and $f(n)$ to be the number of ways to write $n$ as a sum of powers of $2$ where no power occurs more than twice.

For example, $f(10)=5$ since there are five different ways to express $10$:

$10 = 8+2 = 8+1+1 = 4+4+2 = 4+2+2+1+1 = 4+4+1+1$

It can be shown that for every fraction $\dfrac{p}{q} (p>0, q>0)$ there exists at least one integer $n$ such that $\dfrac{f(n)}{f(n-1)}=\dfrac{p}{q}$.

For instance, the smallest $n$ for which $\dfrac{f(n)}{f(n-1)}=\dfrac{13}{17}$ is $241$.

The binary expansion of $241$ is $11110001$.

Reading this binary number from the most significant bit to the least significant bit there are $4$ one’s, $3$ zeroes and $1$ one. We shall call the string $4,3,1$ the *Shortened Binary Expansion* of $241$.

Find the Shortened Binary Expansion of the smallest $n$ for which $\dfrac{f(n)}{f(n-1)}=\dfrac{123456789}{987654321}$.

Give your answer as comma separated integers, without any whitespaces.

## 解决方案

利用前几项查询OEIS，结果为[A002487](https://oeis.org/A002487)（至于式子的推导，已经在169题中给出）。那么对于所有$n>1$，可以写成$f(2n)=f(n),f(2n-1)=f(n)+f(n-1)$，其中$f(0)=0,f(1)=f(2)=1$。

对于同一个$n$下的两个式子作商，有

$$\dfrac{f(2n-1)}{f(2n)}=\dfrac{f(n)+f(n-1)}{f(n)}=1+\dfrac{f(n-1)}{f(n)}$$

通过这个式子，不难发现，当任意一个数$m$满足$f(m-1)>f(m)$时，$m$为奇数，也就是$m$的二进制下最低位为$1$，否则$m$为偶数，最低位为$0$（此时需要将分式的分子分母交换）。$m$接下来的次低位则通过上面的式子的右边的那个分式$\dfrac{f(n-1)}{f(n)}$决定。这启发我们使用辗转相除法解决这个问题。

回到题目中，题目询问的分式是$\dfrac{f(n)}{f(n-1)}$，那么和上面的讨论结果相反：如果当前分数的分子比分母小，那么$n$的低位为$1$，并且用分母减去分子；否则为$0$，用分子减去分母。$n$的数位从后向前填入。

需要注意的是，如果填入的最高位是$0$，那么最高位需要变成$1$。

## 代码

```py
a, b = 123456789, 987654321
ls = []
while a and b:
    if b >= a:
        ls.append((b // a, 1))
        b %= a
    else:
        ls.append((a // b, 0))
        a %= b
if ls[-1][1] == 0:
    x, y = ls[-1]
    ls.pop()
    ls.append((x - 1, 0))
    ls.append((1, 1))
ans = ",".join([str(v[0]) for v in ls[::-1]])
print(ans)

```
