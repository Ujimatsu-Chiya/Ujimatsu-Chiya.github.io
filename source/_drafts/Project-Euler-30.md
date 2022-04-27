---
title: Project Euler 30
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 30
## 题目
### Digit fifth powers
Surprisingly there are only three numbers that can be written as the sum of fourth powers of their digits:
$$1634=1^4+6^4+3^4+4^4$$
$$8208=8^4+2^4+0^4+8^4$$
$$9474=9^4+4^4+7^4+4^4$$

As $1 = 1^4$ is not a sum it is not included.

The sum of these numbers is $1634 + 8208 + 9474 = 19316$.

Find the sum of all the numbers that can be written as the sum of fifth powers of their digits.

## 解决方案

一个$n$位数如果全是$9$，那么其和数位和的$k$次幂为$n\cdot 9^k$。因此一个$n$位数的值绝不会超过$n \cdot 9^k$。

因此，直接枚举$n$位数直接算即可（注意不要超出当前的上限）。

如果$n$满足$10^n>n\cdot 9^k$，那么停止循环退出。因为$9^k$是相加的，比不上指数增长。
## 代码

```py
K = 5
n = 1
ans = 0
while True:
    mx = min(10 ** (n + 1) - 1, n * 9 ** K)
    i = 10 ** n
    if i > n * 9 ** K:
        break
    while i <= mx:
        s, w = 0, i
        while w:
            s += (w % 10) ** K
            w //= 10
        if s == i:
            ans += i
        i += 1
    n += 1
print(ans)
```