---
title: Project Euler 46
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 46
## 题目
### Goldbach’s other conjecture
It was proposed by Christian Goldbach that every odd composite number can be written as the sum of a prime and twice a square

$\begin{aligned}
9 &= 7 + 2×1^2 \\
15 &= 7 + 2×2^2 \\ 
21 &= 3 + 2×3^2 \\
25 &= 7 + 2×3^2 \\
27 &= 19 + 2×2^2 \\
33 &= 31 + 2×1^2\\
\end{aligned}$

It turns out that the conjecture was false.
What is the smallest odd composite that cannot be written as the sum of a prime and twice a square?

## 解决方案

每次先对当前(因变量，函数)进行排序。如果排完序后，发现三个函数值相同，那么说明找到了一个同时是三角形数、五边形数和六角形数的数，如果需要找下一个，就把所有自变量加一。

否则，就将函数值最小的那个函数自变量加一，以此保持三个函数值之间的大小平衡。

## 代码
```py
N = 3


def T(n):
    return (n * (n + 1)) >> 1


def P(n):
    return (n * (3 * n - 1)) >> 1


def H(n):
    return n * (2 * n - 1)


ls = [[1, T], [1, P], [1, H]]

while True:
    ls.sort(key=lambda x: x[1](x[0]))
    if ls[0][1](ls[0][0]) == ls[-1][1](ls[-1][0]):
        N -= 1
        if N == 0:
            ans = ls[0][1](ls[0][0])
            break
        ls[0][0] += 1
        ls[1][0] += 1
        ls[2][0] += 1
    else:
        ls[0][0] += 1
print(ans)

```