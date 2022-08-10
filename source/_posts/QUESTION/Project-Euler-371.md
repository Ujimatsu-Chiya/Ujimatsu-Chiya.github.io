---
title: Project Euler 371
category:
  - Project Euler
tags:
  - 概率
  - 动态规划
mathjax: true
date: 2022-07-12 00:17:14
---

<escape><!-- more --></escape>

# Project Euler 371

## 题目

### Licence plates

Oregon licence plates consist of three letters followed by a three digit number (each digit can be from $[0..9]$).

While driving to work Seth plays the following game:

Whenever the numbers of two licence plates seen on his trip add to $1000$ that's a win.

E.g. $\text{MIC}-012$ and $\text{HAN}-988$ is a win and $\text{RYU}-500$ and $\text{SET}-500$ too (as long as he sees them in the same trip).

Find the expected number of plates he needs to see for a win.

Give your answer rounded to $8$ decimal places behind the decimal point.

**Note:** We assume that each licence plate seen is equally likely to have any three digit number on it.

## 解决方案

令$N=3$，表示号码牌位数。不难想到使用动态规划的思想解决。

这一些数主要分成三块来看：$0,5\cdot 10^{N-1}$，以及其它剩下的数。

当遇到一个数$0$时，那么对当前状态不会产生任何影响。而对于除$5\cdot 10^{N-1}$之外的其它数而言，如果遇到了$x$，那么当只有遇到$1000-x$时才算胜利（注意此时$x\neq 10^N-x$），我们称$x$和$10^N-x$是一对号码牌；但是对于$5\cdot 10^{N-1}$，只要单独遇到两次则胜利。

因此将$5\cdot 10^{N-1}$分开考虑。考虑状态$g(i)(0\le i<5\cdot 10^{N-1})$表示**已经**遇到一次$5\cdot 10^{N-1}$时，并且已经遇到了独立的$i$对号码牌之中的一对，接下来进行游戏的期望轮数。那么就可以写出$g$的递推式如下：

$g(i)=\dfrac{1\cdot g(i)+1\cdot 0+i\cdot g(i)+i\cdot 0+(10^{N}-2i-2)\cdot g(i+1)}{10^N}+1$

其中$5$项分别表示：遇到了一个$0$号牌；再次遇到了一个$5\cdot 10^{N-1}$号牌；遇到了$i$对号码牌中某一对的同一个；遇到了$i$对号码牌中某一对的另外一个；遇到了一对新的号码牌中的一个。

这是一个**有后效性**的动态规划方程，因为状态之间形成了循环的依赖（状态$i$依赖于自身）。不过，这种情况下消除后效性很简单。右边项也是$g(i)$，只需要挪到左边消除就可以完成消除后效性，从而正确计算结果。

为了方便正式状态转移方程，假设存在状态$g(5\cdot 10^{N-1})$,并令其为$0$,整理关于$g$的方程，消除后效性后可以写成:

$$
g(i)=
\left \{\begin{aligned}
  &0  & & \text{if\quad} i=5\cdot 10^{N-1} \\
  &\dfrac{(10^N-2i-2)\cdot g(i+1)+10^N}{10^N-1-i} & & \text{else}
\end{aligned}\right.
$$

类似的，定义状态$f(i)(0\le i<5\cdot 10^{N-1})$表示**已经**遇到一次$5\cdot 10^{N-1}$时，并且已经遇到了独立的$i$对号码牌之中的一对，接下来进行游戏的期望轮数。那么理解了$g$的状递推式，不难写出关于$f$的递推式：

$f(i)=\dfrac{1\cdot f(i)+1\cdot g(i)+i\cdot f(i)+i\cdot 0+(10^{N}-2i-2)\cdot f(i+1)}{10^N}+1$

类似的，整理后可以写成

$$
f(i)=
\left \{\begin{aligned}
  &0  & & \text{if\quad} i=5\cdot 10^{N-1} \\
  &\dfrac{g(i)+(10^N-2i-2)\cdot f(i+1)+10^N}{10^N-1-i} & & \text{else}
\end{aligned}\right.
$$

那么，最终的答案为$f(0)$.

## 代码

```py
N = 3
k = 10 ** N // 2 - 1
f, g = 0, 0
for i in range(k, -1, -1):
    g = ((10 ** N - 2 * i - 2) * g + 10 ** N) / (10 ** N - 1 - i)
    f = (g + (10 ** N - 2 * i - 2) * f + 10 ** N) / (10 ** N - 1 - i)
ans = f
print("{:.8f}".format(ans))

```
