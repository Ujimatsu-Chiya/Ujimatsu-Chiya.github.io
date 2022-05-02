---
title: Project Euler 91
tags:
  - Project Euler
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 91

## 题目

### Right triangles with integer coordinates

The points $P (x_1, y_1)$ and $Q (x_2, y_2)$ are plotted at integer co-ordinates and are joined to the origin, $O(0,0)$, to form $\triangle OPQ$.

![](../images/p091_1.png)

There are exactly fourteen triangles containing a right angle that can be formed when each co-ordinate lies between $0$ and $2$ inclusive; that is, $0 \leq x_1, y_1, x_2, y_2 \leq 2$.

![](../images/p091_2.png)

Given that $0 \leq x_1, y_1, x_2, y_2 \leq 50$, how many right triangles can be formed?

## 解决方案

由于只有$51\times 51-1$个点，因此每次可以枚举出两个点，通过判断向量内积是否为$0$来找出直角。
将枚举出来的三角形的每一条边都视为一个向量，两两做内积，就可以完成判断，找到一个直角三角形。

通过查询OEIS该数列的前几项，发现结果为[A155154](https://oeis.org/A155154)。在PROG一栏中，发现如下信息：

```
(PARI) a(n)=3*n^2+sum(a=1, n, sum(b = 1, n, 2*min(b*gcd(a, b)\a, (n - a)*gcd(a, b)\b) ) ) \\ Yurii Ivanov, Jun 25 2021
```

通过这个信息，可以以$O(n^2\log n)$计算出本题的结果：

$$3n^2+\sum_{a=1}^n\sum_{b=1}^n2\min(\lfloor\frac{b\gcd(a,b)}{a}\rfloor),\lfloor\frac{(n-a)\gcd(a,b)}{b}\rfloor))$$

## 代码

```py
N = 50

def ok(a: complex, b: complex):
    if a.imag * b.imag + a.real * b.real == 0:
        return 1
    u = b - a
    if u.imag * a.imag + u.real * a.real == 0:
        return 1
    v = a - b
    if v.imag * b.imag + v.real * b.real == 0:
        return 1
    return 0


ls = []
for i in range(0, N + 1):
    for j in range(0, N + 1):
        if i + j > 0:
            ls.append(complex(i, j))
ans = 0
for i in range(len(ls)):
    for j in range(i + 1, len(ls)):
        if ok(ls[i], ls[j]):
            ans += 1

print(ans)

```

```py
from tools import gcd

N = 50
ans = 3 * N ** 2
for a in range(1, N + 1):
    for b in range(1, N + 1):
        g = gcd(a, b)
        ans += 2 * min(b * g // a, (N - a) * g // b)
print(ans)

```
