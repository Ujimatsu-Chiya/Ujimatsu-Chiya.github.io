---
title: Project Euler 561
category:
  - Project Euler
tags:
mathjax: true
date: 2022-07-13 22:57:30
---

<escape><!-- more --></escape>

# Project Euler 561

## 题目

### Divisor Pairs

Let $S(n)$ be the number of pairs $(a,b)$ of distinct divisors of $n$ such that $a$ divides $b$.

For $n=6$ we get the following pairs: $(1,2), (1,3), (1,6),( 2,6)$ and $(3,6)$. So $S(6)=5$.

Let $p_m\#$ be the product of the first $m$ prime numbers,  so $p_2\# = 2*3 = 6$.

Let $E(m, n)$ be the highest integer $k$ such that $2^k$ divides $S((p_m\#)^n)$.

$E(2,1) = 0$ since $2^0$ is the highest power of $2$ that divides $S(6)=5$.

Let $Q(n)=\sum_{i=1}^{n} E(904961, i)$

$Q(8)=2714886$.

Evaluate $Q(10^{12})$.

## 解决方案

令$n$的分解质因数为$n=\prod_{i=1}^m p_i^{e_i}$。那么，$S(n)$的求解就化为以下问题：

有多少对$m$维向量$(\vec{a},\vec{b})$，其中$\vec{a}=(a_1,a_2,\dots,a_m),\vec{b}=(b_1,b_2,\dots,b_m)$，满足$\forall i\in[1,m],0\le a_i\le b_i\le e_i$，并且$\vec{a}\neq \vec{b}$？

不难计算出$S(n)=\prod_{i=1}^m \dfrac{(e_i+1)(e_i+2)}{2}-\prod_{i=1}^m (e_i+1)$

计算$S((p_m\#)^n)$时，可以发现$e_1=e_2=\dots=e_m=n$。

因此，

$$S((p_m\#)^n)=\left(\dfrac{(n+1)(n+2)}{2}\right)^m-(n+1)^m$$

当$n$是奇数时，上式可以改写成$S((p_m\#)^n)=\left(\dfrac{n+1}{2}\right)^m((n+2)^m-2^m)$，这确保了第二项是奇数。

当$n$是偶数时，上式可以改写成$S((p_m\#)^n)=(n+1)^m\left(\left(\dfrac{n+2}{2}\right)^m-1\right)$，这时第一项是奇数。

令函数$f(x)$为：最大的一个$e$使得$2^e\mid x$。令$n=4k+a,a\in\{0,1,2,3\}$。接下来描述$a$的$4$种情况，$a$将和上面讨论$S((p_m\#)^n)$的奇偶性对应。

1. 当$a=0$时，代入$S((p_m\#)^n)$的第二项，得到$(2k+1)^m-1$，因式分解后为$2k\cdot \sum_{i=0}^{m-1}(2k+1)^i.$
a. 如果$m$为奇数，那么式子中的求和项有奇数个，因此整个值为奇数，此时$E(n,m)=f(k)+1$.
b. 如果$m$为偶数，那么经过对$(2k+1)^m-1$打表后再找规律，发现$E(n,m)=f(k)+1 +f(k+1)+f(m)$
2. 当$a=1$时，代入$S((p_m\#)^n)$的第一项，得到$(2k+1)^m$，这是个奇数，故$E(m,n)=0.$
3. 当$a=2$时，代入$S((p_m\#)^n)$的第二项，得到$(2k)^m-1$，这是个奇数，故$E(m,n)=0.$
4. 当$a=3$时，代入$S((p_m\#)^n)$的第一项，得到$(2k+2)^m$，那么$E(m,n)=m\cdot f(2k+2)=m\cdot(f(k+1)+1)$.

令$m=904961,N=10^{12}.$那么，有$\left\lfloor\dfrac{N}{4}\right\rfloor$个数属于$a=0$的情况，有$\left\lfloor\dfrac{N+1}{4}\right\rfloor$属于$a=3$种情况。

令$F(n)=\sum_{i=1}^n f(i)$，当$m$为奇数时，有：

$\begin{aligned}
&\sum_{k=0}^{\left\lfloor\frac{N+1}{4}\right\rfloor-1}m\cdot(f(k+1)+1)+\sum_{k=1}^{\left\lfloor\frac{N}{4}\right\rfloor}f(k)+1\\
=&m\cdot F\left(\left\lfloor\dfrac{N+1}{4}\right\rfloor\right)+m\cdot\left\lfloor\dfrac{N+1}{4}\right\rfloor+F\left(\left\lfloor\dfrac{N}{4}\right\rfloor\right)+\left\lfloor\dfrac{N}{4}\right\rfloor
\end{aligned}$

当$m$是偶数时，同样将式子代入即可。

最终的问题则是高效计算$F(n)$。计算的思想使用了容斥原理：在$2^0$的倍数中，有多少个不是$2^1$的倍数，这些数贡献了$0$；在$2^1$的倍数中，有多少个不是$2^2$的倍数，这些数贡献了$1$……，最终，分类将它们的贡献相加即可。

## 代码

```py
N = 10 ** 12
M = 904962


def F(n):
    return sum(((n >> i) - (n >> (i + 1))) * i for i in range(len(bin(n)) - 2))


c0 = N // 4
c3 = (N + 1) // 4
if M % 2 == 0:
    ans = M * F(c3) + M * c3 + F(c0) + c0 + F(c0 + 1) + (bin(M)[::-1].find('1')) * c0
else:
    ans = M * F(c3) + M * c3 + F(c0) + c0
print(ans)

```
