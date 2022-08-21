---
title: Project Euler 721
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 721
## 题目
### High powers of irrational numbers



Given is the function $f(a,n)=\lfloor{(\lceil{\sqrt{a}\:\rceil}+\sqrt{a}\:)^n}\rfloor$.

$\lfloor{.}\rfloor$ denotes the floor function and $\lceil{.}\rceil$ denotes the ceiling function.

$f(5,2)=27$ and $f(5,5)=3935$.

$G(n) = \displaystyle \sum_{a=1}^n f(a, a^2).$

$G(1000) \text{ mod  } 999\,999\,937=163861845. $

Find $G(5\,000\,000).$ Give your answer modulo $999\,999\,937$.




## 解决方案

由于$\lceil\sqrt{a}\:\rceil-\sqrt{a}<1$，并且根据二项式定理展开，补上共轭项消去根号，因此实际上$f(a,n)$可以写成：

$$f(a,n)=(\lceil{\sqrt{a}\:\rceil}+\sqrt{a}\:)^n+(\lceil{\sqrt{a}\:\rceil}-\sqrt{a}\:)^n-1$$

令$g(a,n)=(\lceil{\sqrt{a}\:\rceil}+\sqrt{a}\:)^n+(\lceil{\sqrt{a}\:\rceil}-\sqrt{a}\:)^n$，也就是$g(a,n)=f(a,n)+1$。可以发现，$g(a,n)$为一个关于$n$的二阶线性递推式。因此接下来的思路是将$g(a,n)$写成快速幂形式，再通过矩阵快速幂进行加速计算。

那么，假设这个线性递推式为$g(a,n)=p\cdot g(a,n-1)+q\cdot g(a,n-2)$。移项后可以写成：

$$g(a,n)-p\cdot g(a,n-1)-q\cdot g(a,n-2)=0$$

根据韦达定理，可以得到

$$\left\{\begin{aligned}
&-p=-(\lceil{\sqrt{a}\:\rceil}+\sqrt{a}\:)-(\lceil{\sqrt{a}\:\rceil}-\sqrt{a}\:)\\
&-q=(\lceil{\sqrt{a}\:\rceil}+\sqrt{a}\:)\cdot(\lceil{\sqrt{a}\:\rceil}-\sqrt{a}\:)
\end{aligned}\right.$$

化简后也就是

$$\left\{\begin{aligned}
&p=2\cdot\lceil{\sqrt{a}\:\rceil}\\
&q=a-\lceil{\sqrt{a}\:\rceil}^2
\end{aligned}\right.$$

其中，$g(a,0)=2,g(a,1)=2\cdot\lceil{\sqrt{a}\:\rceil} $。

通过写成如下矩阵形式加速计算，最终将计算出来的$g$回代到$f$中得到结果。
$$
\begin{bmatrix}
g(n-1)\\
g(n)
\end{bmatrix}=
\begin{bmatrix}
0 & 1\\
a-\lceil{\sqrt{a}\:\rceil}^2 & 2\cdot\lceil{\sqrt{a}\:\rceil}
\end{bmatrix}
\cdot 
\begin{bmatrix}
g(n-2)\\
g(n-1)
\end{bmatrix}
$$


## 代码


