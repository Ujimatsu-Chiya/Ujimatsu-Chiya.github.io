---
title: Project Euler 778
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 778
## 题目
### Freshman's Product



If $a,b$ are two nonnegative integers with decimal representations $a=(\dots a_2a_1a_0)$ and $b=(\dots b_2b_1b_0)$ respectively, then the *freshman's product* of $a$ and $b$, denoted $a\boxtimes b$, is the integer $c$ with decimal representation $c=(\dots c_2c_1c_0)$ such that $c_i$ is the last digit of $a_i\cdot b_i$.

For example, $234 \boxtimes 765 = 480$.


Let $F(R,M)$ be the sum of $x_1 \boxtimes \dots \boxtimes x_R$ for all sequences of integers $(x_1,\dots,x_R)$ with $0\leq x_i \leq M$.

For example, $F(2, 7) = 204$, and $F(23, 76) \equiv 5870548 \pmod{ 1\,000\,000\,009}$.


Find $F(234567,765432)$, give your answer modulo $1\,000\,000\,009$



## 解决方案


## 代码


```py
from itertools import count

R = 234567
M = 765432
mod = 1000000009


def cal(n, pos, d):
    pw = 10 ** pos
    ans = n // (pw * 10) * pw
    t = n // pw % 10
    if t > d:
        ans += pw
    elif t == d:
        ans += n % pw + 1
    return ans


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


ans = 0
for p in count(0, 1):
    if 10 ** p > M:
        break
    a = [[0 for _ in range(10)]]
    a[0][1] = 1
    b = [[0 for _ in range(10)] for _ in range(10)]
    for d in range(10):
        k = cal(M, p, d)
        for i in range(10):
            b[i][i * d % 10] += k
    r = R
    while r:
        if r & 1:
            a = mul(a, b)
        b = mul(b, b)
        r >>= 1
    ans += sum(i * a[0][i] for i in range(10)) * (10 ** p)
    ans %= mod
print(ans)

```