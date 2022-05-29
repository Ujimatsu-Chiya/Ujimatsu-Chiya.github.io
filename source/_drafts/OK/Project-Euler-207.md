---
title: Project Euler 207
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 207
## 题目
### Integer partition equations


For some positive integers $k$, there exists an integer partition of the form   $4^t = 2^t + k$, where $4^t, 2^t$ and $k$ are all positive integers and $t$ is a real number.

The first two such partitions are $4^1 = 2^1 + 2$ and $4^{1.5849625\dots} = 2^{1.5849625\dots} + 6$.

Partitions where $t$ is also an integer are called *perfect*.

For any $m \ge 1$ let $P(m)$ be the proportion of such partitions that are perfect with $k \le m$.

Thus $P(6) = 1/2$.

In the following table are listed some values of $P(m)$

$\begin{aligned}
   P(5) &= &1/1 \\
   P(10)& = &1/2 \\
   P(15) &= &2/3 \\
   P(20) &= &1/2 \\
   P(25) &= &1/2 \\
   P(30) &= &2/5 \\
   &\dots&\\
   P(180) &=& 1/4\\
   P(185) &=& 3/13
\end{aligned}$

Find the smallest $m$ for which $P(m) < 1/12345$

## 解决方案

令$x=2^t(x>0)$，那么上面的方程就可以化成$x^2-x=k$。

那么，当$x$为某一个正整数时，$x^2=x+k$就是一个划分，那么$k$就必须满足$k=x^2-x,x=1,2,\dots$。

回到题目中，如果$t$是一个整数，那么$x=2^t$就必须是一个二次幂。

这启发我们先从小到大遍历$x$值，然后再判断$x$值是否为一个二次方数，计算出比率，直接进行判断。

其中，使用如下代码判断一个有符号数$x$是否为一个二次方数：

```
(x & (x - 1)) == 0
```

## 代码


```py
from itertools import count

Q = 12345
cnt = 0
for x in count(2, 1):
    if (x & (x - 1)) == 0:
        cnt += 1
    if cnt * Q < x - 1:
        ans = x * (x - 1)
        break
print(ans)

```