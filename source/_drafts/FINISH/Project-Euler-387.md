---
title: Project Euler 387
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 387
## 题目
### Harshad Numbers


A **Harshad or Niven number** is a number that is divisible by the sum of its digits.

$201$ is a Harshad number because it is divisible by $3$ (the sum of its digits.)

When we truncate the last digit from $201$, we get $20$, which is a Harshad number.

When we truncate the last digit from $20$, we get $2$, which is also a Harshad number.

Let's call a Harshad number that, while recursively truncating the last digit, always results in a Harshad number a *right truncatable Harshad number.*

Also:

$201/3=67$ which is prime.

Let's call a Harshad number that, when divided by the sum of its digits, results in a prime a *strong Harshad number*.

Now take the number $2011$ which is prime.

When we truncate the last digit from it we get $201$, a strong Harshad number that is also right truncatable.

Let's call such primes *strong, right truncatable Harshad primes*.

You are given that the sum of the strong, right truncatable Harshad primes less than $10000$ is $90619$.

Find the sum of the strong, right truncatable Harshad primes less than $10^{14}$.




## 解决方案

令$N=14.$不难发现，$1$位质数不是可右截强Harshad数，因为一位数与自己数位和的商为$1$，不是一个质数。

本题主要关注可右截Harshad数。这种数的有一种生成思想：如果当前数$x$是一个可右截Harshad数，并且$10x+d$（$d$是一个新的数位）也是一个Harshad数，那么$10x+d$就是一个可右截Harshad数。

很明显，$1\sim 9$本身就是可右截Harshad数，将作为起点进行扩展。最终发现，$10^{N-1}$以内的可右截Harshad数的数量不多。

接下来，我们将枚举出来的可右截Harshad数，逐一直接判断是否为强Harshad数，并保留强Harshad数的一部分。

对每个右截强Harshad数$y$，后面都填上$1,3,7,9$这$4$个数位$d$中的一个，那么构造出了$10y+d$。最终如果$10y+d$是质数，那么就添加到答案中。

## 代码


```py
from tools import is_prime

N = 14


def is_harshad(n: int):
    return n % sum(int(x) for x in str(n)) == 0


ls = [[1, 2, 3, 4, 5, 6, 7, 8, 9]]
tp = [1, 3, 7, 9]
for i in range(N - 2):
    ls.append([])
    for x in ls[i]:
        for j in range(10):
            t = x * 10 + j
            if is_harshad(t):
                ls[i + 1].append(t)
ans = 0
for v in ls:
    for n in v:
        if not is_prime(n // sum(int(x) for x in str(n))):
            continue
        for y in tp:
            w = n * 10 + y
            if is_prime(w):
                ans += w
print(ans)

```