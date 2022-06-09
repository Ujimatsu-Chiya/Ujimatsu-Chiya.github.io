---
title: Project Euler 51
tags:
  - Project Euler
mathjax: true
date: 2022-05-03 09:22:28
---

<escape><!-- more --></escape>

# Project Euler 51

## 题目

### Prime digit replacements

By replacing the $1^{st}$ digit of the $2$-digit number $*3$, it turns out that six of the nine possible values: $13, 23, 43, 53, 73$, and $83$, are all prime.

By replacing the $3^{rd}$ and $4^{\th}$ digits of $56**3$ with the same digit, this $5$-digit number is the first example having seven primes among the ten generated numbers, yielding the family: $56003, 56113, 56333, 56443, 56663, 56773,$ and $56993$.

Consequently $56003$, being the first member of this family, is the smallest prime with this property.

Find the smallest prime which, by replacing part of the number (not necessarily adjacent digits) with the same digit, is part of an eight prime value family.

## 解决方案

此处使用一个术语：模板，用来表示题意中带星号和数字的混合字符串。如题目中的$*3,56**3$等。

这些模板通过将对所有星号(*)填入相同的数位，产生$9\sim10$个数（当模板的最高位是星号时，将不能填入$0$）。

一个关于模板的结论：

如果一个模板能够产生$8$个质数，那么这个模板的星号个数必须为$3$的倍数。

设模板中星号的个数为$k$，其余的数字之和为$s$，那么产生的数字的数位和为$s,s+k,s+2k,...,s+9k$。

1. 当$k$满足$k\equiv 0 (\mod 3)$时，可以发现： $s\equiv s+k\equiv s+2k\equiv...\equiv s+9k(\mod 3)$

这种情况下，当$s$*不满足*$s\equiv0(\mod 3)$时，就有可能产生$8$个质数。

2. 否则，总有

$\begin{aligned}
& s\equiv s+3k\equiv s+6k\equiv s+9k(\mod 3) \\
& s+1k\equiv s+4k\equiv s+7k(\mod 3) \\
& s+2k\equiv s+5k\equiv s+8k(\mod 3)
\end{aligned}$

这三条式子中，总存在一条是和$0$是同余的。在这种情况下，就有$3$个合数，不能构造出$8$个质数，所以，原结论成立。

另外，题目要求枚举的质数中，是某个模板下产生的$8$个质数中最小的。因此，所枚举的质数必定是以某个模板填入$0,1,2$这三个数位之一。

因此，利用上面的结论，直接开始枚举质数。

本代码使用sympy库中的nextprime函数，它将返回当前大于数的下一个质数。

## 代码

```py
from sympy import nextprime
from tools import is_prime
from itertools import count, combinations

M = 8
a = [1, 2]


# 将数的一部分下标替换成模板
def change(s: str, pos_list):
    ls = list(s)
    for pos in pos_list:
        ls[pos] = '*'
    return "".join(ls)


def ok(n: int):
    s = str(n)
    # 存放字符串中,0,1,2的下标
    pos = [[], [], []]
    for i in range(len(s)):
        if int(s[i]) <= 2:
            pos[int(s[i])].append(i)
    # 产生星号数为3的倍数的模板
    for stars in count(3, 3):
        candidates = list(combinations(pos[0], stars)) + list(combinations(pos[1], stars)) + list(
            list(combinations(pos[2], stars)))
        if len(candidates) == 0:
            break
        for pos_list in candidates:
            # 用来产生模板t。
            t = change(s, pos_list)
            cnt = 0
            for i in range(10):
                if i == 0 and t[0] == '*':
                    continue
                if is_prime(int(t.replace('*', str(i)))):
                    cnt += 1
            if cnt >= M:
                return True
    return False


pr = 0
while True:
    pr = nextprime(pr)
    if ok(pr):
        ans = pr
        break
print(ans)

```
