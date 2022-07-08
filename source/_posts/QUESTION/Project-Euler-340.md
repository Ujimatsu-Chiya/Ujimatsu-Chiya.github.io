---
title: Project Euler 340
tags:
  - Project Euler
mathjax: true
date: 2022-07-08 17:06:12
---

<escape><!-- more --></escape>

# Project Euler 340

## 题目

### Crazy Function

For fixed integers $a, b, c$, define the *crazy function* $F(n)$ as follows:

$F(n) = n - c$ for all n > b

$F(n) = F(a + F(a + F(a + F(a + n))))$ for all $n \le b$

Also, define $S(a, b, c) = \sum_{n=0}^{b}F(n)$.

For example, if $a = 50, b = 2000$ and $c = 40$, then $F(0) = 3240$ and $F(2000) = 2040$. Also, $S(50, 2000, 40) = 5204240$.
Find the last $9$ digits of $S(21^7, 7^{21}, 12^7)$.

## 解决方案

本题主要依靠多次调整$a,b,c$的值，利用python来打印出函数的图像来推测$F$的表达式。

用以下代码打印一部分的图像，以$a=12,b=30,c=7$为例打印$F$的形状：

```py
import matplotlib.pyplot as plt

a, b, c = 12, 30, 7


def f(n):
    if n > b:
        return n - c
    else:
        return f(a + f(a + f(a + f(a + n))))


X = [i for i in range(b + b)]
Y = list(map(f, X))
fig, ax = plt.subplots()
ax.scatter(X, Y)
plt.show()

```

![](../images/p340-1.png)

最终发现了以下一些特点：

1. 从$b$往前起，每$a$个点视作一块。在每一块的内部，函数值都是递增的，并且恰好为$1$。块内的和可以使用等差数列之和不难计算出来。
2. 从$b$往前起的每一块，对应函数值都会增长$3a-3c$。也就是说，$F(n)=b+4(a-c)$，那么$F(n-a)=b+(a-c),F(n-2a)=b-2(a-c),\dots$，那么块间也是等差数列就可以计算得出。不过，最左边一块不是完整的一块，需要单独计算。

以$b-a+1\sim b$这一块开始，通过等差数列公式可以计算出$t_0=\sum_{i=b-a+1}^b F(i)=\dfrac{a(2b+7a-8c+1)}{2}$

那么计算块间之和。可以发现一共有$m=\lfloor\dfrac{b+1}{a}\rfloor$块，并且首项为$t_0$，公差为$a\cdot(3a-3c)$。再次通过等差数列公式计算出这一些完整的块的$F$值之和。

剩下的不完整的块中有$(b+1)\%a$个元素，单独计算即可。

## 代码

```py
a, b, c = 21 ** 7, 7 ** 21, 12 ** 7
mod = 10 ** 9


def cal(l, d, n):
    return n * (l + l + (n - 1) * d) // 2


block, res = divmod(b + 1, a)
t0 = cal(b + 4 * (a - c), -1, a)
ans = cal(t0, a * (3 * a - 3 * c), block)
ans += cal(b + 4 * (a - c) + block * 3 * (a - c), -1, res)
ans %= mod
print(ans)

```
