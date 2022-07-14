---
title: Project Euler 686
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 686

## 题目

### Powers of Two

$2^7=128$ is the first power of two whose leading digits are "$12$".

The next power of two whose leading digits are "$12$" is $2^{80}$.

Define $p(L, n)$ to be the $n\text{th}$-smallest value of $j$ such that the base $10$ representation of $2^j$ begins with the digits of $L$.

So $p(12, 1) = 7$ and $p(12, 2) = 80$.

You are also given that $p(123, 45) = 12710$.

Find $p(123, 678910)$.

## 解决方案

将$2^k$对$10$进行取对数，那么得到$k\log_{10} 2$。如果$2^k$是以$123$为开头，那么$k\log_{10}2$的小数部分$d=k\log _{10}2-\lfloor k\log_{10}2\rfloor$满足$\log_{10}1.23\le d<\log_{10} 1.24$。因此，最朴素的一种做法是从小到大枚举$k$，观察$k\log_{10}2$的小数部分是否落在那个区间上即可。这个区间写成小数形式为：

$[0.08990511143939793,0.09342168516223506)\qquad(1)$

这个区间的长度为$0.0035165737228371324$

不过，朴素枚举区间的效率比较慢。暴力枚举出前一部分项后，发现相邻的两项差值总在集合$S=\{196, 289, 485\}$中。

可以发现这几个数有以下特征：

$\begin{aligned}
&196\log_{10}2=59+0.00187915014031\\
&289\log_{10}2=87-0.002331253109431941\\
&485\log_{10}2=146-0.00045210296912046033
\end{aligned}$

后面的尾数都很小，比上面的区间长度都小。假设当前$2^a$是一个答案，也就是说，$a\log_{10}2$的小数部分$x$在区间$(1)$内。那么，

- 当$x\in[0.08990511143939793,0.09342168516223506-0.00187915014031)$时，对$a$相加$196$，那么就找到了下一个答案。
- 当$x\in[0.08990511143939793+0.002331253109431941,0.09342168516223506)$时，对$a$相加$289$，那么就找到了下一个答案。
- 当$x\in[0.08990511143939793+0.00045210296912046033,0.09342168516223506)$时，对$a$相加$485$，那么就找到了下一个答案。

并且发现，这三个条件所包括的区间的**并**，和原来的区间$(1)$是相同的。因此对于每个答案$a$，只需要对集合$S$中的数，从小到大尝试一遍，都将会找到答案。

枚举到第一个答案为$90$，因此从这个答案开始寻找。

注意在实现过程中，多次计算$a\log _{10}2$时，不要使用累加，因为这将会将浮点数误差累积起来。

## 代码

```py
from math import log10

N = 678910
l, r = log10(1.23), log10(1.24)
lg = log10(2)
s = [196, 289, 485]
ans = 90
for _ in range(N - 1):
    for j in range(len(s)):
        val = (ans + s[j]) * lg
        if l <= val - int(val) < r:
            ans += s[j]
            break
    if j == len(s):
        print("FAIL")
        exit()
print(ans)

```