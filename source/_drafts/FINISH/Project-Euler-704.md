---
title: Project Euler 704
tags:
  - Project Euler
  - OEIS
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 704

## 题目

### Factors of Two in Binomial Coefficients

Define $g(n, m)$ to be the largest integer $k$ such that $2^k$ divides $\binom{n}m$.

For example, $\binom{12}5 = 792 = 2^3 \cdot 3^2 \cdot 11$, hence $g(12, 5) = 3$.

Then define $F(n) = \max \{ g(n, m) : 0 \le m \le n \}$. $F(10) = 3$ and $F(100) = 6$.

Let $S(N)$ = $\displaystyle\sum_{n=1}^N{F(n)}$. You are given that $S(100) = 389$ and $S(10^7) = 203222840$.

Find $S(10^{16})$.

## 解决方案

枚举$F$的前几项，观察到以下序列：

```
0
1 0
2 1 2 0
3 2 3 1 3 2 3 0
4 3 4 2 4 3 4 1 4 3 4 2 4 3 4 0
5 4 5 3 5 4 5 2 5 4 5 3 5 4 5 1 5 4 5 3 5 4 5 2 5 4 5 3 5 4 5 0
6 5 6 4 6 5 6 3 6 5 6 4 6 5 6 2 6 5 6 4 6 5 6 3 6 5 6 4 6 5 6 1 6 5 6 4
```

将第$F(2^i)\sim F(2^{i+1}-1)$全部放在一行，可以看到每一行其实是将上一行的所有值都加一，再复制一次拼接在自身后面（除了最后的$0$）。

因此，直接通过规律写出并化简关于$S$的递推式：

$$
S(n)=
\left \{\begin{aligned}
  &0 & & \mathrm{if\quad} n=1 \\
  &(i-3)\cdot 2^i+i+3 & & \mathrm{else if\quad} ∃i,2^i-1=n \\
  &S(f(n))+S(n-\dfrac{f(n)+1}{2})-S(\dfrac{f(n)-1}{2})+n-f(n) & & \mathrm{else if\quad} n\le \dfrac{3f(n)+1}{2} \\
  &2S(f(n))-2S(\dfrac{f(n)-1}{2})+S(n-f(n)-1)+n-f(n)& & \mathrm{else}
\end{aligned}\right.
$$

其中，$f(n)$是小于等于$n$的最大的形如$2^i-1$的数。

OEIS相关序列：[A119387](https://oeis.org/A119387)

## 代码

```py
N = 10 ** 16


def S(n):
    fn = (1 << ((n + 1).bit_length() - 1)) - 1
    if fn == n:
        i = (n + 1).bit_length() - 1
        return (i - 3) * 2 ** i + i + 3
    elif n * 2 <= 3 * fn + 1:
        return S(fn) + S(n - ((fn + 1) >> 1)) - S((fn - 1) >> 1) + n - fn
    else:
        return S(fn) * 2 - S((fn - 1) >> 1) * 2 + S(n - fn - 1) + n - fn


ans = S(N)
print(ans)

```
