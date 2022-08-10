---
title: Project Euler 169
category:
  - Project Euler
tags:
  - 动态规划
  - OEIS
mathjax: true
date: 2022-05-11 19:27:32
---

<escape><!-- more --></escape>

# Project Euler 169

## 题目

### Exploring the number of different ways a number can be expressed as a sum of powers of 2

Define $f(0)=1$ and $f(n)$ to be the number of different ways n can be expressed as a sum of integer powers of $2$ using each power no more than twice.

For example, $f(10)=5$ since there are five different ways to express $10$:

$\begin{aligned}
& 1 + 1 + 8\\
& 1 + 1 + 4 + 4\\
& 1 + 1 + 2 + 2 + 4\\
& 2 + 4 + 4\\
& 2 + 8
\end{aligned}$

What is $f(10^{25})$?

## 解决方案

如果$n$是一个奇数，那么就可以从$n$划分出一个$1=2^0$出来，然后再从$n-1$中继续进行。但注意这时$n-1$不能够再从$2^0$继续划分了，因为再用$2^0$就相当于用了$3$次$2^0$，不合题意。因此只能从$2^1$开始寻找，而这等价于值为$\dfrac{n-1}{2}$的一个新问题。

如果$n$是一个偶数，那么可以选择不将$2^0=1$分出来，直接从$2^1$开始找，这等价于值为$\dfrac{n}{2}$的一个新问题；也可以选择将两个$2^0$分出来，再从剩下的$n-2$那一部分开始尝试将$2^1$划分出来，这等价于值为$\dfrac{n-2}{2}$的新问题。

因此，假设$f(i)(i>0)$为题目中要求的划分数，可以列出如下状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &1  & & \text{if\quad} i=1 \\
  &f\left(\dfrac{i-1}{2}\right) & & \text{else if\quad} i \equiv 1 \pmod 2 \\
  &f\left(\dfrac{i}{2}\right)+f\left(\dfrac{i-2}{2}\right)  & & \text{else}
\end{aligned}\right.
$$

为避免子问题的重复计算，代码实现使用了记忆化搜索。

另外，用前几项查询OEIS，结果为[A002487](https://oeis.org/A002487)。

## 代码

```py
N = 10 ** 25
mp = {}


def dfs(n: int):
    if n <= 1:
        return 1
    if n in mp.keys():
        return mp[n]
    m = n >> 1
    if n & 1:
        mp[n] = dfs(m)
    else:
        mp[n] = dfs(m) + dfs(m - 1)
    return mp[n]


ans = dfs(N)
print(ans)
```
