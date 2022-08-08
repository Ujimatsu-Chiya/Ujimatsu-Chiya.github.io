---
title: Project Euler 111
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-06 22:23:58
---

<escape><!-- more --></escape>

# Project Euler 111

## 题目

### Primes with runs

Considering $4$-digit primes containing repeated digits it is clear that they cannot all be the same: $1111$ is divisible by $11$, $2222$ is divisible by $22$, and so on. But there are nine $4$-digit primes containing three ones:

$$1117, 1151, 1171, 1181, 1511, 1811, 2111, 4111, 8111$$

We shall say that $M(n, d)$ represents the maximum number of repeated digits for an $n$-digit prime where $d$ is the repeated digit, $N(n, d)$ represents the number of such primes, and $S(n, d)$ represents the sum of these primes.

So $M(4, 1) = 3$ is the maximum number of repeated digits for a $4$-digit prime where one is the repeated digit, there are $N(4, 1) = 9$ such primes, and the sum of these primes is $S(4, 1) = 22275$. It turns out that for $d = 0$, it is only possible to have $M(4, 0) = 2$ repeated digits, but there are $N(4, 0) = 13$ such cases.

In the same way we obtain the following results for $4$-digit primes.

|$\mathbf{Digit, d}$|$\mathbf{M(4, d)}$|$\mathbf{N(4, d)}$|$\mathbf{S(4, d)}$|
|-|-|-|-|
|$0$|$2$|$13$|$67061$|
|$1$|$3$|$9$|$22275$|
|$2$|$3$|$1$|$2221$|
|$3$|$3$|$12$|$46214$|
|$4$|$3$|$2$|$8888$|
|$5$|$3$|$1$|$5557$|
|$6$|$3$|$1$|$6661$|
|$7$|$3$|$9$|$57863$|
|$8$|$3$|$1$|$8887$|
|$9$|$3$|$7$|$48073$|

For $d = 0$ to $9$, the sum of all $S(4, d)$ is $273700$.

Find the sum of all $S(10, d)$.

## 解决方案

本题主要通过位运算的手段来枚举。

这里用一个$N$比特数$mask$表示一个$N$位数的状态。对于某个数位$d(0\leq d\leq 9)$，如果任意一个$N$位数，第$i$位为$d$，那么状态$mask$的第$i$位为$1$，否则为$0$。

以题目中的数字为例，如$d=1,N=4$时，$1117$表示成状态$(1110)_2$，$2111$为状态$(0111)_2$。

将所有的$N$比特状态值枚举出来，将状态按其中比特为$1$的数量$b$进行分类。

按照比特为$1$的数量$b$，从大到小枚举每个分类，遍历分类中所有的状态，然后通过递归生成对应状态$mask$下的所有数。在这些拥有$b$个某数位$d$的数中，如果存在一个数是质数，那么就有$M(N,d)=b$，第一次找到的结果就是最优的。找完其它有$b$个$d$的质数后，那么循环就可以停下来，不用再往后判断$b-1$个$d$的那些数了。

另外，还需要注意最高位不能填$0$这种情况。

## 代码

```py
from tools import is_prime

N = 10

ls = [[] for i in range(N)]
for s in range(1, (1 << N) - 1):
    ls[bin(s).count('1')].append(s)


def gen(msk: int, f: int, digit: int, num: int, a: list):
    if f == -1:
        if isprime(num):
            a.append(num)
        return
    if msk >> f & 1:
        if digit == 0 and f == N - 1:
            return
        else:
            gen(msk, f - 1, digit, num * 10 + digit, a)
    else:
        # 如果是在最高位任意填，那么必须从1开始填，否则从0开始填。
        for k in range(int(f == N - 1), 10):
            if k != digit:
                gen(msk, f - 1, digit, num * 10 + k, a)


ans = 0
for digit in range(10):
    for bits in range(N - 1, 0, -1):
        a = []
        for v in ls[bits]:
            gen(v, N - 1, digit, 0, a)
        s = sum(a)
        if s:
            ans += s
            break
print(ans)

```
