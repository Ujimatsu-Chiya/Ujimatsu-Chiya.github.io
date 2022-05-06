---
title: Project Euler 103
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:26
---

<escape><!-- more --></escape>

# Project Euler 103

## 题目

### Special subset sums: optimum

Let $S(A)$ represent the sum of elements in set $A$ of size $n$. We shall call it a special sum set if for any two non-empty disjoint subsets, $B$ and $C$, the following properties are true:

1. $S(B) \neq S(C)$; that is, sums of subsets cannot be equal.
2. If $B$ contains more elements than $C$ then $S(B) > S(C)$.

If $S(A)$ is minimised for a given $n$, we shall call it an optimum special sum set. The first five optimum special sum sets are given below.

$\begin{aligned}
n = 1&: \{1\} \\
n = 2&: \{1, 2\} \\
n = 3&: \{2, 3, 4\} \\
n = 4&: \{3, 5, 6, 7\} \\
n = 5&: \{6, 9, 11, 12, 13\} \\
\end{aligned}$

It *seems* that for a given optimum set, $A = {a_1, a_2, \dots , a_n}$, the next optimum set is of the form  $B = {b, a_1+b, a_2+b, \dots ,a_n+b}$, where $b$ is the "middle" element on the previous row.

By applying this "rule" we would expect the optimum set for $n=6$ to be $A = \{11, 17, 20, 22, 23, 24\}$, with $S(A) = 117$. However, this is not the optimum set, as we have merely applied an algorithm to provide a near optimum set. The optimum set for $n=6$ is $A = \{11, 18, 19, 20, 22, 25\}$, with $S(A) = 115$ and corresponding set string: $111819202225$.

Given that $A$ is an optimum special sum set for $n=7$, find its set string.

NOTE: This problem is related to <a href="problem=105">Problem 105</a> and <a href="problem=106">Problem 106</a>.

## 解决方案

一个推论：如果一个集合满足题目中的第一个条件，那么它们的所有$2^n$个子集$I$的$S(I)$都不相同。

使用反证法：设一个集合$A$，对于$A$中的两个子集$I,J$，满足$S(I)=S(J)$，有以下两种情况

1. $I \bigcap J = \emptyset$：那么明显$A$集合不符合要求。
2. $I \bigcap J \neq \emptyset$：此时取$I'=I-J,J'=J-I$，根据集合差运算的定义，有$S(I')=S(I)-S(I \bigcap J),S(J')=S(J)-S(I \bigcap J)$。可以知道，此时$I' \bigcap J' = \emptyset$，但有$S(I')=S(J')$，不符合要求。

因此原推论成立，判断集合是否为特殊不需要直接枚举一对不相交子集。而是产生所有子集，先判断元素和是否重复，然后根据和的大小进行排序比较集合大小即可（判断第二个条件是否满足）。

题目中介绍了一个生成特殊集合的方法，但不保证元素和是最小的。

因此，个人思路如下：

1. 利用题目中给定的方法暂时生成一个$n=7$的特殊集合$A$
2. 对集合中的每个元素施加一定的“扰动”（每个元素都先让它们加一或减一或不动），由此尝试找到元素和更小的特殊集合。

## 代码

```py
from itertools import product

a = [11, 18, 19, 20, 22, 25]
b = [a[len(a) // 2]]
for x in a:
    b.append(20 + x)
n = len(b)
ans = list(b)


def ok(z: list):
    mp = {}
    for st in range(1 << n):
        cnt, s = 0, 0
        for i in range(n):
            if st >> i & 1:
                cnt += 1
                s += z[i]
        if s in mp.keys():
            return False
        mp[s] = cnt
    ls = list(mp.items())
    ls.sort()
    for i in range((1 << n) - 1):
        if ls[i][1] > ls[i + 1][1]:
            return False
    return True


for w in product([-1, 0, 1], repeat=n):
    z = [w[i] + b[i] for i in range(n)]
    if sum(z) < sum(ans) and ok(z):
        ans = z
print("".join([str(x) for x in ans]))

```
