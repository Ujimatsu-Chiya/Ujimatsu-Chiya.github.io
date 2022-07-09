---
title: Project Euler 375
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 375
## 题目
### Minimum of subsequences


Let $S_n$ be an integer sequence produced with the following pseudo-random number generator:
$$
\begin{aligned}
S_0  &= 290797 \\
S_{n+1}  &= S_n^2 \mod 50515093
\end{aligned}
$$


Let $A(i, j)$ be the minimum of the numbers $S_i, S_{i+1}, \ldots, S_j$ for $i\le j$.

Let $M(N) = \sum A(i, j)$ for $1 \le i \le j \le N$.

We can verify that $M(10) = 432256955$ and $M(10\,000) = 3264567774119$.


Find $M(2\,000\,000\,000)$.

## 单调栈

单调栈是一种数据结构，栈内元素保证单调性。这种数据结构用于维护这个序列中，每一个数在左边/右边比它大/小的第一个数。

如果要求某个数右边比它第一个大的数，那么考虑从右往左遍历序列。对于每一个数，弹出栈中比它小的所有数。如果栈未空，那么栈顶的数就是答案，否则说明这个数右边没有比它大的数。最终把自身压入这个栈中。

## 解决方案

注意到，$S$是一个周期序列，其周期$T=6308948$，最小值为$m=3$.

对于这道题，我们考虑这个序列中每一个数$S_i$能够对答案$M(N)$。这启发我们先使用单调栈找出每一个数$S_i$分别在左边和右边严格比它小的第一个数$S_l,S_r$。那么对于所有区间$[i,j],l < i\le j< r$，区间$[i,j]$都是以$S_i$为最小值，这些区间一共有$(r-i)\cdot (i-l)$个。另外，注意到$S$是周期序列，因此对$S_{i+T}$而言，也会有同样类似的结论。

如果最小值$m$是某个区间的贡献，那么$m$可能横跨多个区间。为了避免重复计算，接下来先考虑比$m$大的数的贡献。

由于$S$有周期性，因此为了能够方便求解这个问题，我们只考虑$S$的前$2T+N\%T$项，对这些项使用上面提到的单调栈算法两次，分别求出两个关于$i$的序列$l[i],r[i]$。

接下来我们将原序列$S$中的$N$个值分成三部分，分别是：$S$的前$T$个数，$S$的最后$T$个数，以及中间其它数。因为前$T$个数中，有可能$l[i]$不存在；对于后$N$个数而言，有可能$r[i]$不存在。

因此对前$T$个数和后$T$个数分别独立计算求和。对于中间剩下的这一部分数，我们就考虑它在这$$


## 代码


