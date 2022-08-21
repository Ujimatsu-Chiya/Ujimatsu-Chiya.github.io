---
title: Project Euler 760
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 760
## 题目
### Sum over Bitwise Operators


Define
$$\displaystyle g(m,n) = (m\oplus n)+(m\vee n)+(m\wedge n)$$
where $\oplus, \vee, \wedge$ are the bitwise XOR, OR and AND operator respectively.

Also set
$$\displaystyle G(N) = \sum_{n=0}^N\sum_{k=0}^n g(k,n-k)$$
For example, $G(10) = 754$ and $G(10^2) = 583766$.

Find $G(10^{18})$. Give your answer modulo $1\,000\,000\,007$.



## 解决方案

给定关于运算$\oplus,\lor,\land$的真值表：

$$\begin{array}{|c|c|c|c|c|}
\hline
 m & n & \oplus & \lor & \land \\
\hline
0 & 0 & 0 & 0 & 0\\
\hline
0 & 1 & 1 & 1 & 0\\
\hline
1 & 0 & 1 & 1 & 0\\
\hline
1 & 1 & 0 & 1 & 1\\
\hline
\end{array}$$

因此，$g(m,n)=2 (n\lor m)$。

## 代码


