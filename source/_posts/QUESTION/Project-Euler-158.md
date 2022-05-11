---
title: Project Euler 158
tags:
  - Project Euler
mathjax: true
date: 2022-05-11 19:28:03
---

<escape><!-- more --></escape>

# Project Euler 158

## 题目

### Exploring strings for which only one character comes lexicographically after its neighbour to the left

Taking three different letters from the $26$ letters of the alphabet, character strings of length three can be formed.

Examples are ‘abc’, ‘hat’ and ‘zyx’.

When we study these three examples we see that for ‘abc’ two characters come lexicographically after its neighbour to the left.

For ‘hat’ there is exactly one character that comes lexicographically after its neighbour to the left. For ‘zyx’ there are zero characters that come lexicographically after its neighbour to the left.

In all there are $10400$ strings of length $3$ for which exactly one character comes lexicographically after its neighbour to the left.

We now consider strings of $n \leq 26$ different characters from the alphabet.

For every $n, p(n)$ is the number of strings of length $n$ for which exactly one character comes lexicographically after its neighbour to the left.

What is the maximum value of $p(n)$?

## 解决方案

可以把满足题意的长度为$n$的单词抽象成一个$n$阶置换。而且，这个置换，由两个下降子数组拼接而成。其中第二个子数组的起点值大于第一个子序列的终点。如图中黑色字符表示的数所示：

![](../images/p158-1.png)

设状态$f(i)(i\ge 1)$为：考虑有多少个$i$阶置换$p$，使得仅存在一个$j(2\le j \le i)$，满足$p[j-1]<p[j]$。

可以得到状态转移方程：

$$
f(i)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} i=1 \\
  &2f(i-1)+i-1  & & \mathrm{else}
\end{aligned}\right.
$$

对于最后一行，我们可以考虑成将一个最大的数$i$插入一个已经构造好的$i-1$阶置换中。因此，对于$2f(i-1)$，$i$可以有两个选择：分别插在两个子数组的顶端（如上图两个红色的O）。

对于$i-1$，则是对于一个逆序的$i-1$阶置换而言，$i$可以分别选择放在这$i-1$个数后面，从而构成两个下降子序列，有$i-1$种方法。

因此，最终答案只需要将$f(n)$乘一个组合数进行比较即可。

## 代码

```py
from tools import get_pascals_triangle

N = 26
C = get_pascals_triangle(N)
f = [0 for i in range(N+1)]
ans = 0
for i in range(1, N):
    f[i] = f[i - 1] * 2 + i - 1
    ans = max(ans, f[i] * C[N][i])
print(ans)

```
