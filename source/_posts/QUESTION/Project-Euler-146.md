---
title: Project Euler 146
tags:
  - Project Euler
mathjax: true
date: 2022-05-10 13:47:41
---

<escape><!-- more --></escape>

# Project Euler 146

## 题目

### Investigating a Prime Pattern

The smallest positive integer $n$ for which the numbers $n^2+1, n^2+3, n^2+7, n^2+9, n^2+13$, and $n^2+27$ are consecutive primes is $10$. The sum of all such integers n below one-million is $1242490$.

What is the sum of all such integers n below $150$ million?

## 解决方案

第一步预处理：

假设质数$p$和非负整数$r(0\le r< p)$，如果对于以及任意非负整数$k$，存在$b\in\{1,3,7,9,13,27\}$，有$p|(kp+r)^2+b$，也就是$p|r^2+b$。那么所有满足$n\equiv r(\mod p)$的$n$都可以排除。

根据这个规律，代入$p=2,3,5,7$，可以排除许多$n$，留下来的$n$一定满足以下所有条件：

$\begin{aligned}
& n\equiv 0(\mod 2)\\
& n\equiv 1 \text{ or }2(\mod 3)\\
& n\equiv 0(\mod 5)\\
& n\equiv 3 \text{ or }4(\mod 7)
\end{aligned}$

那么可以留下大约$\dfrac{2}{105}$个$n$。根据[中国剩余定理](https://mathworld.wolfram.com/ChineseRemainderTheorem.html)，可以认为只有以下$n$才满足条件：

$n\equiv 10\text{ or } 80\text{ or } 130\text{ or } 200(\mod 210)$

第二部预处理：由于sympy库中的素性测试算法isprime对于小数的效率非常低，但是对于大数很高，因此这里利用一些小质数对以上这些$n^2+b$的数进行试除，筛选掉一些合数，减低后面使用isprime的次数。

筛选完成后，正式对这些$n^2+b$使用素性测试算法，统计所有素性测试都能通过的$n$。

还需要注意的一点是，题目要求这六个质数是连续的。

## 代码

```py
from itertools import count

from tools import get_prime, is_prime

N = 150000000
pr = get_prime(11, 33)
s = [1, 3, 7, 9, 13, 27]
# residues = []
# for i in range(210):
#     if i % 2 == 0 and i % 3 != 0 and i % 5 == 0 and i % 7 in [3, 4]:
#         residues.append(i)

residues = [10, 80, 130, 200]
candidate = []

for n in count(0, 210):
    if n > N:
        break
    for res in residues:
        w = n + res
        flag = True
        for q in pr:
            for x in s:
                if (w * w + x) % q == 0:
                    flag = False
                    break
            if not flag:
                break
        if flag:
            candidate.append(w)
ans = 0
for n in candidate:
    if n > N:
        break
    flag = True
    for x in s:
        if not is_prime(n * n + x):
            flag = False
            break
    if flag:
        cnt = 0
        for i in range(1, 28, 2):
            if is_prime(n * n + i):
                cnt += 1
        if cnt != len(s):
            flag = False
    if flag:
        ans += n
print(ans)

```
