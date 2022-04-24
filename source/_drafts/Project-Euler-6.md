---
title: Project Euler 6
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 6
## 题目
### Sum square difference

The sum of the squares of the first ten natural numbers is,
$$1^2 + 2^2 + ... + 10^2 = 385$$
The square of the sum of the first ten natural numbers is,
$$(1 + 2 + ... + 10)^2 = 55^2 = 3025$$
Hence the difference between the sum of the squares of the first ten natural numbers and the square of the sum is $3025 - 385 = 2640$.
Find the difference between the sum of the squares of the first one hundred natural numbers and the square of the sum.

## 解决方案

两个公式：

前n个数的平方和为$\frac{n(n+1)(2n+1)}{6}$.
前n个数的和为$\frac{n(n+1)}{2}$.

直接代入公式并计算。

## 代码

```Python
n = 100
ans = (n * (n + 1) // 2) ** 2 - n * (n + 1) * (2 * n + 1) // 6
print(ans)
```