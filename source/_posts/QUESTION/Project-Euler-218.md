---
title: Project Euler 218
category:
  - Project Euler
tags:
mathjax: true
date: 2022-06-05 09:29:05
---

<escape><!-- more --></escape>

# Project Euler 218

## 题目

### Perfect right-angled triangles

Consider the right angled triangle with sides $a=7, b=24$ and $c=25$. The area of this triangle is $84$, which is divisible by the perfect numbers $6$ and $28$.

Moreover it is a primitive right angled triangle as $\gcd(a,b)=1$ and $\gcd(b,c)=1$.

Also $c$ is a perfect square.
We will call a right angled triangle perfect if

- it is a primitive right angled triangle
- its hypotenuse is a perfect square

We will call a right angled triangle super-perfect if

- it is a perfect right angled triangle and
- its area is a multiple of the perfect numbers $6$ and $28$.

How many perfect right-angled triangles with $c\le10^{16}$ exist that are not super-perfect?

## 解决方案

本题一个让人出乎意料之外的地方是，题目要求的三角形并不存在。也就是说，答案为$0$。

接下来证明这个过程：

勾股数组$(a,b,c)$的产生。枚举一系列的二元组$(s,t)$，其中$s>t$，那么可以产生勾股数组$(2st,s^2-t^2,s^2+t^2)$。

由于$c$是一个完全平方数，那么存在一个数$m,c=m^2$，那么也就是有$s^2+t^2=m^2$，而这恰好又是一个勾股数组，因此，我们使用$p,q(p>q)$来产生勾股数组$(s,t,m)$。那么$s=\max(2pq,p^2-q^2),t=\min(2pq,p^2-q^2)$。

因此，

$\begin{aligned}
& a=2st=4pq(p^2-q^2)\\
& b=s^2-t^2=|(p^2-q^2)^2-4p^2q^2|=|p^4+q^4-6p^2q^2|
\end{aligned}$

那么三角形的面积为

$$S=\dfrac{1}{2}ab=2pq(p^2-q^2)|p^4+q^4-6p^2q^2|$$

接下来是三个部分的证明：$3\mid S,4\mid S,7\mid S$。因为$\text{lcm}(6,28)=84=2^2\times 3\times 7$，遵循一致的证明方法。需要注意的是，式子中的所有变量，除了项$pq$，都是以平方的出现。

### $3\mid S$

如果$p$或$q$是$3$的倍数，那么结论成立。

对于任意的$x\in \mathbb{N}$，发现$x^2\% 3 \in\{0,1\}$。

如果$p^2\%3=q^2\%3=1$，那么$(p^2-q^2)\%3=0$，原结论成立。

### $4\mid S$

注意到，$S$有个常数因子$2$。

如果$p$或$q$是$2$的倍数，那么结论成立。

对于任意的$x\in \mathbb{N}$，发现$x^2\% 2 \in\{0,1\}$。

如果$p^2\%2=q^2\%2=1$，那么$(p^2-q^2)\%2=0$，原结论成立。

### $7\mid S$

如果$p$或$q$是$7$的倍数，那么结论成立。

对于任意的$x\in \mathbb{N}$，发现$x^2\% 7 \in\{0,1,2,4\}$。

如果$p^2\%7=q^2\%7$，那么$(p^2-q^2)\%2=0$，原结论成立。

不失一般性，

如果$p^2\%7=1,q^2\%7=2$，那么$(p^4+q^4-6p^2q^2)\%7=0$

如果$p^2\%7=1,q^2\%7=4$，那么$(p^4+q^4-6p^2q^2)\%7=0$

如果$p^2\%7=2,q^2\%7=4$，那么$(p^4+q^4-6p^2q^2)\%7=0$

因此，$7\mid S$。

最终，$84\mid S$，因此题目所求三角形并不存在。

## 代码

```py
print(0)
```
