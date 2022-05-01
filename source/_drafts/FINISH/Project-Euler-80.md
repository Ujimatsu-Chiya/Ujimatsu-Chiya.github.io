---
title: Project Euler 80
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 80
## 题目
### Square root digital expansion
It is well known that if the square root of a natural number is not an integer, then it is irrational. The decimal expansion of such square roots is infinite without any repeating pattern at all.

The square root of two is $1.41421356237309504880\ldots$, and the digital sum of the first one hundred decimal digits is $475$.

For the first one hundred natural numbers, find the total of the digital sums of the first one hundred decimal digits for all the irrational square roots.


## 解决方案

在计算机中，小数只能通过浮点数近似，不能精确表示，但是整数可以精确表示。因此本题尝试将小数部分“转移”到整数部分再计算整数上的平方根。

容易发现这么一个规律：$10\sqrt n=\sqrt{100n}$。这说明，只要我们需要求前$n$位小数时，我们只需要将这个整数乘$10^{2n}$，再计算整数下的平方根后，原本的$n$位小数就转移到了整数部分的最后$n$位，并且能精确表示。

以下面一个为例：
为$\sqrt{2}$求小数点后面$2$位，发现：
$\sqrt{2}=1.41421356237309504880\ldots$
$\lfloor\sqrt{2}\rfloor=1$
$\sqrt{20000}=141.421356237309504880\ldots$
$\lfloor\sqrt{20000}\rfloor=\lfloor100\sqrt{2}\rfloor=141$

本题使用了gmpy2库中的is_square函数，用于判断当前的数是否为平方数。这个函数将封装在自定义的tools工具包中。

另一种方法则是使用牛顿迭代法，此处不再赘述。

## 代码

```py
from gmpy2 import is_square
from tools import int_sqrt

ans = 0
N = 100
M = 100
for i in range(2, N + 1):
    if is_square(i):
        continue
    w = int_sqrt(i * 10 ** (2 * M))
    ans += sum(int(x) for x in str(w)[:M])
print(ans)

```