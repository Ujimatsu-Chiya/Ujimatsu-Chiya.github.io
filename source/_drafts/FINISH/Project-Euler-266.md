---
title: Project Euler 266
tags:
  - Project Euler
  - meet-in-the-middle
mathjax: true
---
<escape><!-- more --></escape>
    



# Project Euler 266
## 题目
### Pseudo Square Root

The divisors of $12$ are: $1,2,3,4,6$ and $12$.

The largest divisor of $12$ that does not exceed the square root of $12$ is $3$.

We shall call the largest divisor of an integer $n$ that does not exceed the square root of $n$ the pseudo square root ($\text{PSR}$) of $n$.

It can be seen that $\text{PSR}(3102)=47$.

Let $p$ be the product of the primes below $190$. Find $\text{PSR}(p) \mod 10^{16}$.


## 解决方案

质数的个数只有$m=42$个，比较容易想到meet-in-the-middle思想。

令$n$为这些质数的积。前$21$个质数可以产生$n$的因子的一部分，存放在数组$lm$中，后$21$个质数也可以产生$n$的因子的另一部分，放在数组$rm$中。


那么，$lm,rm$中任意一对数的乘积组合就一一对应了$n$的因子。

因此在$lm$中，每遍历一个数$x$，就在$rm$中找到一个最大的$y$，使得$xy\le \sqrt{N}$。

采用排序后用双指针进行遍历的方法就可以完成这个问题。

## 代码

```py
from tools import int_sqrt, get_prime

N = 190
mod = 10 ** 16
pr = get_prime(N)
lm, rm = [1], [1]
for p in pr[:len(pr) >> 1]:
    lm += [x * p for x in lm]
for p in pr[len(pr) >> 1:]:
    rm += [x * p for x in rm]
sq = int_sqrt(lm[-1] * rm[-1])
lm.sort()
rm.sort()
r = len(rm) - 1
ans = 0
for l in range(len(lm)):
    while r >= 0 and lm[l] * rm[r] > sq:
        r -= 1
    if r < 0:
        break
    ans = max(ans, lm[l] * rm[r])
ans %= mod
print(ans)

```

