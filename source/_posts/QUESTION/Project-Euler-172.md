---
title: Project Euler 172
tags:
  - Project Euler
mathjax: true
date: 2022-05-15 10:15:59
---

<escape><!-- more --></escape>

# Project Euler 172

## 题目

### Investigating numbers with few repeated digits

How many $18$-digit numbers $n$ (without leading zeros) are there such that no digit occurs more than three times in $n$?

## 多重全排列公式

多重全排列公式：假设使用$r_1$个**相同**元素$c_1$，$r_2$个相同元素$c_2$，$\dots$，$r_n$个相同元素$c_n$，那么可以构成以下数量的**不同**全排列个数：

$$\dfrac{(\sum_{i=1}^nr_i)!}{\prod_{i=1}^nr_i!}$$

## 解决方案

由于每个数位最多使用$3$次，因此分别枚举有$i,j,k,h(h+i+j+k=10)$个数位使用了$1$次，$2$次，$3$次，或者没有使用。由此，现在问题变成了两个**独立**的子步骤：这$i,j,k,h$个数位对应到$10$个数位，有多少种对应方式？当数位对应好后，有多少个排列？

第一个步骤：分配各个数位的对应次数的数量为$C_{10}^i\cdot C_{10-i}^j\cdot C_{10-i-j}^k=\dfrac{10!}{i!\cdot j!\cdot k!\cdot h!}$。

第二个步骤：使用多重全排列公式，可以得到$\dfrac{N!}{(0!)^h\cdot(1!)^i\cdot(2!)^j\cdot(3!)^k}$。

两个步骤前后相互独立，故相乘。

注意这里要求不包括前导$0$，由于每一个数位填在最高位的概率都是平等的，因此最终答案需要乘个$\dfrac{9}{10}$。

## 代码

```py
N = 18
M = max(N, 10)
fac = [1]
for i in range(1, M + 1):
    fac.append(fac[-1] * i)
ans = 0
for i in range(11):
    for j in range(11 - i):
        for k in range(11 - i - j):
            if i + 2 * j + 3 * k == N:
                h = 10 - i - j - k
                a = fac[N] // 2 ** j // 6 ** k
                c = fac[10] // fac[h] // fac[i] // fac[j] // fac[k]
                ans += a * c

ans = ans * 9 // 10
print(ans)
```
