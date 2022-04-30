---
title: Project Euler 48
tags:
  - Project Euler
mathjax: true
date: 2022-04-27 23:32:54
---

<escape><!-- more --></escape>

# Project Euler 48

## 题目

### Self powers

The series, $1^1 + 2^2 + 3^3 + … + 10^{10} = 10405071317$.

Find the last ten digits of the series, $1^1 + 2^2 + 3^3 + \dots + 1000^{1000}$.

## 解决方案

快速幂算法，可以在$O(\log m)$的时间复杂度内计算$a^m \mod p$的值。

Python代码如下：

```py
def quick_power(a: int, m: int, p: int):
    ans = 1
    while m > 0:
        if m & 1:
            ans = ans * a % p
        a = a * a % p
        m >>= 1
    return ans
```

这个算法本质上是将幂$m$看作是二进制位。

并且，$a^{2^i}$可以很容易地由$a^{2^{i-1}}$计算出：$a^{2^i}=(a^{2^{i-1}})^2$。

因此，将幂指数$m$看作是二进制数，如果第$i$位上是$1$，那么就将结果乘上$a^{2^i}$。将所有值累乘起来就得到答案。

由于Python自带pow(a,m,p)，因此直接调用即可。

## 代码

## Q48

```Python
N = 1000
mod = 10000000000
ans = 0
for i in range(1, N + 1):
    ans = (ans + pow(i, i, mod)) % mod
print("{:09}".format(ans))

```
