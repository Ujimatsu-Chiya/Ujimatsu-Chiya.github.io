---
title: Project Euler 118
tags:
  - Project Euler
  - 动态规划
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 118
## 题目
### Pandigital prime sets


Using all of the digits $1$ through $9$ and concatenating them freely to form decimal integers, different sets can be formed. Interestingly with the set $\{2,5,47,89,631\}$, all of the elements belonging to it are prime.

How many distinct sets containing each of the digits one through nine exactly once contain only prime elements?

## 解决方案

本题的第一个目标：找出所有数字使用最多一次的质数，并对使用完全相同数位的质数进行统计，统计结果记录在列表$cnt$中。

在这里，用一个$9$比特的$mask$（下标从$0$开始）来表示数位使用情况，如果数字$i$被使用了，那么$mask$的第$i-1$位为$1$，否则为$0$。

一个例子：$13$和$31$都是质数，因此$mask=2^0+2^2=5，cnt[5]=2$。

因此，通过一些枚举技巧，可以将一些不可能是质数的情况排除，从而能够加速快速枚举完质数。

得到了$cnt$数组后，进行第二步：动态规划。

需要注意到问题所要求的集合是无序的，因此可以使用动态规划来求出满足的集合数很方便。

这里使用的是状态压缩动态规划。设$f(i,st)$为：使用了$[0,i]$中所有的$mask$下对应的数后，当前有多少个集合的数位使用情况为$st$？也就是说，有多少集合，已经使用了$1,2,\dots,9$里面的一些数了。如上面提到，$st$是一个$9$比特数。

可以列出如下状态转移方程：

$$
f(i,st)=
\left \{\begin{aligned}
  &1  & & \mathrm{if\quad} i=0\&st=0 \\
  &0  & & \mathrm{else if\quad} i=0 \\
  &f(i-1,st)  & & \mathrm{else if\quad} st\&i\neq i \\
  &f(i-1,st)+f(i-1,st \bigoplus i) \times cnt[i] & & \mathrm{else}
\end{aligned}\right.
$$

其中，运算符$\&,\bigoplus $分别表示位运算中的与运算和异或运算。

方程最后一行表示，如果不取$i$，那么直接从$f(i-1,st)$转移过来保存；如果取$i$，那么就需要将没有用到$i$的前驱状态再添加一个$mask$属于$i$类中的数，而这类数有$cnt[i]$个。

最终答案为$f(2^9-1,2^9-1)$。

代码中的实现则为另一种方式，它是以“我为人人”的方式实现的，即将当前状态转移到所有的后继可能的状态，这种写法会比较方便和好想。

## 代码

```py
from itertools import permutations, combinations
from tools import is_prime

a = [1, 2, 3, 4, 5, 6, 7, 8, 9]
n = len(a)
cnt = [0 for i in range(1 << n)]
cnt[1 << (2 - 1)] = cnt[1 << (3 - 1)] = cnt[1 << (5 - 1)] = 1
for r in range(1, n + 1):
    for st in combinations(a, r):
        if sum(st) % 3 == 0:
            continue
        mask = 0
        for x in st:
            mask |= 1 << (x - 1)
        for per in permutations(st):
            if (per[-1] & 1) == 0 or per[-1] == 5:
                continue
            w = int("".join(str(x) for x in per))
            if is_prime(w):
                cnt[mask] += 1

f = [0 for i in range(1 << n)]
f[0] = 1
for i in range(1 << n):
    if cnt[i] > 0:
        for j in range(1 << n):
            if (j & i) == 0:
                f[i | j] += f[j] * cnt[i]

print(f[(1 << n) - 1])

```

