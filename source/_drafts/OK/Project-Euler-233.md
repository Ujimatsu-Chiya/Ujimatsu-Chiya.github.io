---
title: Project Euler 233
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 233
## 题目
### Lattice points on a circle

Let $f(N)$ be the number of points with integer coordinates that are on a circle passing through $(0,0), (N,0),(0,N),$ and $(N,N)$.

It can be shown that $f(10000)=36$.

What is the sum of all positive integers $N\le10^{11}$ such that $f(N)=420$?


## 解决方案

可以写出这个圆的标准方程：

$$(x-\dfrac{N}{2})^2+(y-\dfrac{N}{2})^2=\dfrac{N^2}{2}$$

$$(2x-N)^2+(2y-N)^2=2N^2$$

令$a=2x-N,b=2y-N$，那么转而寻求以下方程的解：

$$a^2+b^2=2N^2$$

不难发现，$a,b$的奇偶性一定相同。并且，$a,b$的奇偶性必须和$N$都相同，因为$x=\dfrac{a+N}{2},y=\dfrac{b+N}{2}$。只有如此，$x,y$才是整数。

不过，可以证明，$a^2+b^2=2N^2$的解$(a,b)$奇偶性一定和$N$相同，上面的问题不需要考虑。用反证法，假设$a,b$的奇偶性和$N$不同，得出方程两边的数奇偶性不同即可。

那么，剩下的问题就只需要考虑这个方程的解的个数即可：

$$x^2+y^2=2N^2$$

[页面1](https://en.wikipedia.org/wiki/Sum_of_squares_function#Formulae#)，[页面2](https://mathworld.wolfram.com/SumofSquaresFunction.html)给出了一个信息：如果$n$可以将其分解成$n=2^g\prod_i p_i^{e_i}\prod_j q_j^{f_j}$，其中$p_i$是模$4$余$1$的质数，$q_j$是模$4$余$3$的质数。那么方程$x^2+y^2=n$的解的个数由$r_2(n)$决定：

$$r_2(n)=
\left \{\begin{aligned}
  &0  & & \mathrm{if\quad} ∃j,f_j\equiv 1(\mod 2) \\
  &4\prod_i(e_i+1) & & \mathrm{else}
\end{aligned}\right.
$$

回到题目中，那么$f(n)$可以如下计算：

$$f(n)=r_2(2n^2)=4\prod_i(2e_i+1)$$

由于$420=4\cdot3\cdot 5\cdot 7$，因此，题目所求的$n$有如下$5$种形式：

$$\begin{aligned}
&Q\cdot P_1\cdot P_2^2\cdot P_3^3\\
&Q\cdot P_1\cdot P_2^{17}\\
&Q\cdot P_1^2\cdot P_2^{10} \\
&Q\cdot P_1^{3}\cdot P_2^{7}\\
&Q\cdot P_1^{57}
\end{aligned}$$

其中，$Q$是模$4$余$3$的质数之积，$P_i$是模$4$余$1$的质数。
## 代码


