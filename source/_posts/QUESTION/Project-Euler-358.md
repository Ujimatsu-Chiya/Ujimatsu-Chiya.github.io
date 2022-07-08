---
title: Project Euler 358
tags:
  - Project Euler
mathjax: true
date: 2022-07-08 17:05:51
---

<escape><!-- more --></escape>

# Project Euler 358

## 题目

### Cyclic numbers

A **cyclic number** with $n$ digits has a very interesting property:

When it is multiplied by $1, 2, 3, 4, \dots n$, all the products have exactly the same digits, in the same order, but rotated in a circular fashion!

The smallest cyclic number is the $6$-digit number $142857$ :

$\begin{aligned}
142857 \times 1 = 142857\\
142857 \times 2 = 285714\\
142857 \times 3 = 428571\\
142857 \times 4 = 571428\\
142857 \times 5 = 714285\\
142857 \times 6 = 857142
\end{aligned}$

The next cyclic number is $0588235294117647$ with $16$ digits :

$\begin{aligned}
&0588235294117647 \times 1 = 0588235294117647\\
&0588235294117647 \times 2 = 1176470588235294\\
&0588235294117647 \times 3 = 1764705882352941\\
&\dots\\
&0588235294117647 \times 16 = 9411764705882352\\
\end{aligned}$

Note that for cyclic numbers, leading zeros are important.

There is only one cyclic number for which, the eleven leftmost digits are $00000000137$ and the five rightmost digits are $56789$ (i.e., it has the form $00000000137\dots56789$ with an unknown number of digits in the middle). Find the sum of all its digits.

## 解决方案

本解决方案参考了[循环数](https://en.wikipedia.org/wiki/Cyclic_number)页面的部分内容。

循环数和以质数为分母的分数单位$\dfrac{1}{p}$息息相关。在$b$进制下，如果分数$\dfrac{1}{p}$以小数形式的循环节长度为$p-1$，那么$\dfrac{1}{p}$的前$p-1$位小数组合起来就是一个$b$进制下的循环数。

此外还提到，如果$\dfrac{1}{p}$在$b$进制下的循环节长度为$p-1$，那么$b$是群$\mathbb{Z}_p^{\star}$的[原根](https://en.wikipedia.org/wiki/Primitive_root_modulo_n)。

最终，通过一个质数$p$和一个满足条件的进制数$b$，可以构造出一个循环数$c(b,p)=\dfrac{b^{p-1}-1}{p}$.假设进制$b$为$10$，那么$f(b,p)\cdot p$恰好为$b^{p-1}-1$，数位和为$9(p-1)$。分拆$f(b,p)\cdot p=f(b,p)+f(b,p)\cdot(p-1)$，注意到这两个数$f(b,p)$实际上是$f(b,p)\cdot(p-1)$的数位逆序，因此这两个数相等，最终循环数$f(b,p)$的数位和是$\dfrac{(b-1)(p-1)}{2}$.

由于这个数的开头是$00000000137$，那么所需要寻找的质数$p$满足$0.00000000137\le\dfrac{1}{p}<0.00000000138$.在这个范围内进行寻找。

为了加速程序运行，质数判断和原根判断是最慢的两个过程，应该放在后面判断。我们**假设**目前枚举出来的数$p$是个质数，那么根据$f(n,p)\cdot p=b^{p-1}-1$，判断$p$是否满足$56789\cdot p\%10^5=10^5-1$，如果是那么再进行剩下两个过程的判断。另外一方面，通过第一个判断的概率非常小，这足以让程序能够快速运行。

## 代码

```py
from math import floor, ceil
from sympy import is_primitive_root
from tools import phi, is_prime

left = "00000000137"
right = "56789"
val = float("0." + left)
ed = floor(1 / val)
val += 10 ** -len(left)
st = ceil(1 / val)
right_v = int(right)
mod = 10 ** len(right)
mod_1 = mod - 1
ph = phi(mod)
p = st - 1

for p in range(st | 1, ed + 1, 2):
    if right_v * p % mod == mod_1 and is_prime(p) and is_primitive_root(10, p):
        ans = (p - 1) // 2 * 9
        break
print(ans)

```
