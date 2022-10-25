---
title: Project Euler 156
category:
  - Project Euler
tags:
mathjax: true
date: 2022-05-15 10:16:11
---

<escape><!-- more --></escape>

# Project Euler 156

## 题目

### Counting Digits

Starting from zero the natural numbers are written down in base 10 like this:
$0\ 1\ 2\ 3\ 4\ 5\ 6\ 7\ 8\ 9\ 10\ 11\ 12\ \dots.$

Consider the digit d=1. After we write down each number n, we will update the number of ones that have occurred and call this number f(n,1). The first values for f(n,1), then, are as follows:

|$n$|$f(n,1)$|
|-|-|
|$0$|$0$|
|$1$|$1$|
|$2$|$1$|
|$3$|$1$|
|$4$|$1$|
|$5$|$1$|
|$6$|$1$|
|$7$|$1$|
|$8$|$1$|
|$9$|$1$|
|$10$|$2$|
|$11$|$4$|
|$12$|$5$|

Note that $f(n,1)$ never equals $3$.

So the first two solutions of the equation $f(n,1)=n$ are $n=0$ and $n=1$. The next solution is $n=199981$.

In the same manner the function $f(n,d)$ gives the total number of digits d that have been written down after the number $n$ has been written.

In fact, for every digit $d \neq 0$, $0$ is the first solution of the equation $f(n,d)=n$.

Let $s(d)$ be the sum of all the solutions for which $f(n,d)=n$.

You are given that $s(1)=22786974071$.

Find  $\sum s(d)$ for $1 \leq d \leq 9$.

Note: if, for some $n$, $f(n,d)=n$ for more than one value of $d$ this value of $n$ is counted again for every value of $d$ for which $f(n,d)=n$.

## 解决方案

$f(n,d)$可以以$O(\log n)$的时间复杂度被计算出来。具体计算方法是计算每个数位下$d$的贡献，不过这里需要一些实现细节。

可以发现，方程$f(n,d)=n$的解明显不超过$10^{12}$。因为在此之后的数，当$n$增加$1$，$f(n,d)$增加的**期望**超过$1$（为$\dfrac{n}{10}$，可以假设每个数位被选中某个数的概率是相等的)，$f(n,d)$和$n$的差距只会越来越大。($10^{10}\sim10^{12}$这一部分数用于保证边缘值被找到。)

枚举$n$，如果$n$和$f(n,d)$相等，那么找到了一个解。否则为了尽快弥补差距，可以假设接下来的数的所有数位都是（不是）$d$，那么可以对$n$增加$\left\lfloor\dfrac{|n-f(n,d)|}{\left\lfloor\log_{10}n\right\rfloor+1}\right\rfloor$。

需要注意的是，每到达一个$10^m$（$10$的幂），$n$的数位就多$1$。因此，为了避免$10^m$附近的数被跳过忽略，每次都从$10^m$开始枚举，到达$10^{m+1}$时结束枚举。

容易发现这种枚举方式效率较高，很快得出答案。

## 代码

```py
N = 12


def f(n: int, d: int):
    ans = 0
    i = 1
    while n // i:
        j = n // i
        high = j // 10
        if d == 0:
            if high:
                high -= 1
            else:
                break
        ans += high * i
        tp = j % 10
        if tp > d:
            ans += i
        elif tp == d:
            ans += n - j * i + 1
        i *= 10
    return ans


pw = [1]
for i in range(N):
    pw.append(pw[-1] * 10)
ans = 0
for j in range(1, 9 + 1):
    i = 1
    lg = 0
    while i <= pw[-2]:
        v = abs(i - f(i, j))
        if v == 0:
            ans += i
            i += 1
        else:
            i += (v + lg) // (lg + 1)
            if i >= pw[lg + 1]:
                lg += 1
                i = pw[lg]

print(ans)
```
