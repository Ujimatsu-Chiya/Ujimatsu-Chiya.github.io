---
title: Project Euler 66
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>

# Project Euler 66
## 题目
### Diophantine equation
Consider quadratic Diophantine equations of the form:

$$x^2 – Dy^2 = 1$$

For example, when $D=13$, the minimal solution in $x$ is $649^2 – 13×180^2 = 1$.

It can be assumed that there are no solutions in positive integers when D is square.

By finding minimal solutions in $x$ for $D = \{2, 3, 5, 6, 7\}$, we obtain the following:

$$\begin{aligned}
3^2 – 2×2^2 = 1 \\
2^2 – 3×1^2 = 1 \\
9^2 – 5×4^2 = 1 \\
5^2 – 6×2^2 = 1 \\
8^2 – 7×3^2 = 1 \\
\end{aligned}$$

Hence, by considering minimal solutions in $x$ for $D \leq 7$, the largest $x$ is obtained when $D=5$.

Find the value of $D \leq 1000$ in minimal solutions of $x$ for which the largest value of $x$ is obtained.
