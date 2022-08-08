---
title: Project Euler 624
category:
  - Project Euler
tags:
  - 矩阵快速幂
  - 马尔科夫链
mathjax: true
date: 2022-07-27 23:50:43
---

<escape><!-- more --></escape>

# Project Euler 624

## 题目

### Two heads are better than one

An unbiased coin is tossed repeatedly until two consecutive heads are obtained. Suppose these occur on the $(M-1)\text{th}$ and $M\text{th}$ toss.

Let $P(n)$ be the probability that $M$ is divisible by $n$. For example, the outcomes HH, HTHH, and THTTHH all count towards $P(2)$, but THH and HTTHH do not.

You are given that $P(2) =\frac 3 5$ and $P(3)=\frac 9  {31}$. Indeed, it can be shown that $P(n)$ is always a rational number.

For a prime $p$ and a fully reduced fraction $\frac a b$, define $Q(\frac a b,p)$ to be the smallest positive $q$ for which $a \equiv b q \pmod{p}$.
For example $Q(P(2), 109) = Q(\frac 3 5, 109) = 66$, because $5 \cdot 66 = 330 \equiv 3 \pmod{109}$ and $66$ is the smallest positive such number.

Similarly $Q(P(3),109) = 46$.

Find $Q(P(10^{18}),1\,000\,000\,009)$.

## 解决方案

令$N=10^{18}$。使用马尔科夫链来考虑本问题。

这个马尔科夫链一共有$3$个状态：$0,1,2$。其中第$i$个状态表示硬币已经连续抛出了两次正面。

不过实际上，由于状态$2$在正式计算之前都不计入，因此我们接下来实际计算时抛弃了状态$2$，直到第$M-1$步时，我们再假设进入了状态$2$。那么可以写出如下状态转移矩阵：

$$
A=
\begin{bmatrix}
0.5 &0.5\\
0.5 &0
\end{bmatrix}
$$

其中第$i$行第$j$列表示从状态$i$转移到状态$j$的概率。

令列向量$b=(1,0)^T$。因为一开始在状态$0$。那么列向量$b_k=A^kb$就表示进行了$k$步转移后，处在每一个状态的概率分布情况。

将$b_k$向量的计算过程进一步改写，得：

$$
b_k=A^kb=\begin{bmatrix}
0.5 &0.5\\
0.5 &0
\end{bmatrix}^kb=\dfrac{1}{2^k}
\begin{bmatrix}
1 &1\\
1 &0
\end{bmatrix}\cdot b$$

通过经验发现，这个矩阵是计算斐波那契数列$a_0=0,a_1=1,a_n=a_{n-1}+a_{n-2},n\ge 2$的矩阵形式。列向量$b_k$的第二维恰好是$\dfrac{a_k}{2^k}$.

令$\phi_{+}=\dfrac{1+\sqrt{5}}{2},\phi_{-}=\dfrac{1-\sqrt{5}}{2}$。

假设$g(k)$表示经过$k$轮后，首次到达状态$2$的概率值。那么可以写出：

$$g(k)=\dfrac{1}{2}\cdot \dfrac{a_{k-1}}{2^{k-1}}=\dfrac{1}{2\sqrt{5}}((\dfrac{\phi_{+}}{2})^{k-1} -(\dfrac{\phi_{-}}{2})^{k-1})$$

其中不难知道为$a_n=\dfrac{1}{\sqrt{5}}(\phi_{+}^{n} -\phi_{-}^n)$.

那么根据定义可以得到：

$$\begin{aligned}
P(n)&=\sum_{k=1}^{+\infty} g(nk)=\sum_{k=1}^{+\infty} \dfrac{1}{2\sqrt{5}}((\dfrac{\phi_{+}}{2})^{nk-1} -(\dfrac{\phi_{-}}{2})^{nk-1}) \\
&=\dfrac{1}{2\sqrt{5}}\cdot (\dfrac{(\dfrac{\phi_{+}}{2})^{n-1}}{1-(\dfrac{\phi_{+}}{2})^n}-\dfrac{(\dfrac{\phi_{-}}{2})^{n-1}}{1-(\dfrac{\phi_{-}}{2})^n})&\qquad(1)\\
&=\dfrac{1}{\sqrt{5}}\cdot (\dfrac{\phi_{+}^{n-1}}{2^n-\phi_{+}^n}-\dfrac{\phi_{-}^{n-1}}{2^n-\phi_{-}^n})\\
&=\dfrac{1}{\sqrt{5}}\cdot\dfrac{2^n(\phi_{+}^{n-1}-\phi_{-}^{n-1})+\sqrt{5}\cdot(-1)^{n-1}}{2^{2n}-2^n\cdot(\phi_{+}^n+\phi_{-}^n)+(-1)^n}\\
&=\dfrac{2^na_{n-1}+(-1)^{n-1}}{2^{2n}-2^n\cdot b_{n}+(-1)^n}&\qquad(2)\\
\end{aligned}$$

其中$b$序列是$b_0=2,b_1=1,b_n=b_{n-1}+b_{n-2},n\ge 2$，递推式与斐波那契数列一样。

因此通过矩阵快速幂，直接计算出$a_{N-1},b_N$的值。计算完成后，代入$(2)$其中直接求逆元即可。

由于$5$是$1000000009$的二次剩余，因此直接代入$(1)$也可以做完运算。

## 代码

```py
from sympy import mod_inverse

N = 10 ** 18
mod = 1000000009


def mul(a: list, b: list):
    return [[sum(a[i][k] * b[k][j] for k in range(len(b))) % mod for j in range(len(b[0]))] for i in range(len(a))]


b = [[0, 1], [1, 1]]
a = [[0, 1]]
c = [[2, 1]]
m = N - 1
n = N
while n:
    if m & 1:
        a = mul(a, b)
    if n & 1:
        c = mul(c, b)
    b = mul(b, b)
    m >>= 1
    n >>= 1

num = pow(2, N, mod) * a[0][0] + pow(-1, N - 1, mod)
den = pow(2, N + N, mod) - pow(2, N, mod) * c[0][0] + pow(-1, N, mod)
ans = num * mod_inverse(den, mod) % mod
print(ans)

```

```py
from sympy import mod_inverse, sqrt_mod

N = 10 ** 18
mod = 1000000009
sq5 = sqrt_mod(5, mod)
inv2 = mod_inverse(2, mod)
p1 = (1 + sq5) * inv2 * inv2 % mod
p2 = (1 - sq5) * inv2 * inv2 % mod
d1 = pow(p1, N - 1, mod) * mod_inverse(1 - pow(p1, N, mod), mod) % mod
d2 = pow(p2, N - 1, mod) * mod_inverse(1 - pow(p2, N, mod), mod) % mod
ans = mod_inverse(sq5, mod) * inv2 * (d1 - d2) % mod
print(ans)

```
