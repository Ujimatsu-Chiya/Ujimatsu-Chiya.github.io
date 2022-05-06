---
title: Project Euler 106
tags:
  - Project Euler
mathjax: true
date: 2022-05-06 22:23:38
---

<escape><!-- more --></escape>
    
# Project Euler 106
## 题目
### Special subset sums: meta-testing


Let $S(A)$ represent the sum of elements in set $A$ of size $n$. We shall call it a special sum set if for any two non-empty disjoint subsets, $B$ and $C$, the following properties are true:

1. $S(B) \neq S(C)$; that is, sums of subsets cannot be equal.
2. If $B$ contains more elements than $C$ then $S(B) > S(C)$.

For this problem we shall assume that a given set contains n strictly increasing elements and it already satisfies the second rule.

Surprisingly, out of the $25$ possible subset pairs that can be obtained from a set for which $n = 4$, only $1$ of these pairs need to be tested for equality (first rule). Similarly, when $n = 7$, only $70$ out of the $966$ subset pairs need to be tested.

For $n = 12$, how many of the $261625$ subset pairs that can be obtained need to be tested for equality?

NOTE: This problem is related to <a href="/103">Problem 103</a> and <a href="/105">Problem 105</a>.

## 解决方案

由于已经假定了集合$A$已经满足了第二个条件，因此，只需要考虑两个集合$B,C$大小相同（$|B|=|C|=k$）时的情形。

容易发现，不需要求和的情形是：对于 $\forall i:1\leq i\leq k$，$B$中的第$i$小元素**都**小于（或大于）$C$中的第$i$小元素。在最后得出需要求和的时候，需要将这部分情形减去，留下的则计入答案。

因此，首先需要从$A$中选取$2k$个元素，其中$k$个分给$B$集合，另外$k$个分给$C$。由于$B,C$的先后不需要关心，因此一共有$\dfrac{C_{2k}^k}{2}$种分法。

下一个问题的正式描述：已知集合中有$2k$个不同的元素，其中$k$个分给$B$集合，另外$k$个分给$C$。（不失一般性，）对于 $\forall i:1\leq i\leq k$，$B$中的第$i$小元素**都**小于$C$中的第$i$小元素，有多少种划分方法？

为解决这个问题，先以一个例子说明：

设$k=3$，那么就将$1\sim 6$这$6$个数进行放入集合$B$和$C$中。

如果第$i$个数放入$B$中，那么字符串第$i$位记为左圆括号'('，否则记为右圆括号')'。

那么有$5$种方法：

|括号字符串|$B$|$C$|
|-|-|-|
|()()()|$\{1,3,5\}$|$\{2,4,6\}$|
|()(())|$\{1,3,4\}$|$\{2,5,6\}$|
|(())()|$\{1,2,5\}$|$\{3,4,6\}$|
|((()))|$\{1,2,3\}$|$\{4,5,6\}$|
|(()())|$\{1,2,4\}$|$\{3,5,6\}$|

每个括号字符串对应着一种分配方法。可以发现这个括号字符串有一下特点：
1. 左圆括号和右圆括号的数量相等
2. 每个字符串的前缀中，**左圆括号的数量不会少于右圆括号**。这也就说明了，$B$中的每一个数，$C$中总有更大的数和它们一一对应。

符合这种特征的字符串的个数，称为[卡特兰数](https://mathworld.wolfram.com/CatalanNumber.html)，在OEIS中为[A000108](https://oeis.org/A000108)。第$n$项为$C(n)=\dfrac{C_{2n}^n}{n+1}$。

综上所述，答案为：

$$\sum_{k=1}^{\lfloor\dfrac{n}{2}\rfloor}C_n^{2k}(\dfrac{C_{2k}^k}{2}-\dfrac{C_{2k}^k}{k+1})$$

## 代码


```py
from tools import C

N = 12
ans = sum(C(N, 2 * k) * (C(2 * k, k) // 2 - C(2 * k, k) // (k + 1)) for k in range(1, N // 2 + 1))
print(ans)

```