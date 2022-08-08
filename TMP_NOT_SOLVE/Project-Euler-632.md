---
title: Project Euler 632
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 632
## 题目
### Square prime factors


For an integer $n$, we define the <i>square prime factors</i> of $n$ to be the primes whose square divides $n$. For example, the square prime factors of $1500=2^2 \times 3 \times 5^3$ are $2$ and $5$.

Let $C_k(N)$ be the number of integers between $1$ and $N$ inclusive with exactly $k$ square prime factors. You are given some values of $C_k(N)$ in the table below.


\[\begin{array}{|c|c|c|c|c|c|c|}
\hline

&amp; k = 0 &amp; k = 1 &amp; k = 2 &amp; k = 3 &amp; k = 4 &amp; k = 5 \\
\hline
N=10 &amp; 7 &amp; 3 &amp; 0 &amp; 0 &amp; 0 &amp; 0 \\
\hline
N=10^2 &amp; 61 &amp; 36 &amp; 3 &amp; 0 &amp; 0 &amp; 0 \\
\hline
N=10^3 &amp; 608 &amp; 343 &amp; 48 &amp; 1 &amp; 0 &amp; 0 \\
\hline
N=10^4 &amp; 6083 &amp; 3363 &amp; 533 &amp; 21 &amp; 0 &amp; 0 \\
\hline
N=10^5 &amp; 60794 &amp; 33562 &amp; 5345 &amp; 297 &amp; 2 &amp; 0 \\
\hline
N=10^6 &amp; 607926 &amp; 335438 &amp; 53358 &amp; 3218 &amp; 60 &amp; 0 \\
\hline
N=10^7 &amp; 6079291 &amp; 3353956 &amp; 533140 &amp; 32777 &amp; 834 &amp; 2 \\
\hline
N=10^8 &amp; 60792694 &amp; 33539196 &amp; 5329747 &amp; 329028 &amp; 9257 &amp; 78 \\
\hline
\end{array}\]


Find the product of all non-zero $C_k(10^{16})$. Give the result reduced modulo $1\,000\,000\,007$.



# Project Euler 632
## 题目
### Square prime factors

For an integer $n$, we define the <i>square prime factors</i> of $n$ to be the primes whose square divides $n$. For example, the square prime factors of $1500 = 2^2 \times 3 \times 5^3$ are $2$ and $5$.
Let $C_k(N)$ be the number of integers between $1$ and $N$ inclusive with exactly $k$ square prime factors. You are given some values of $C_k(N)$ in the table below.
<table>
<thead>
<tr>
<th align="center"></th>
<th align="center">$k=0$</th>
<th align="center">$k=1$</th>
<th align="center">$k=2$</th>
<th align="center">$k=3$</th>
<th align="center">$k=4$</th>
<th align="center">$k=5$</th>
</tr>
</thead>
<tbody><tr>
<td align="center">$N=10$</td>
<td align="center">$7$</td>
<td align="center">$3$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
</tr>
<tr>
<td align="center">$N=10^2$</td>
<td align="center">$61$</td>
<td align="center">$36$</td>
<td align="center">$3$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
</tr>
<tr>
<td align="center">$N=10^3$</td>
<td align="center">$608$</td>
<td align="center">$343$</td>
<td align="center">$48$</td>
<td align="center">$1$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
</tr>
<tr>
<td align="center">$N=10^4$</td>
<td align="center">$6083$</td>
<td align="center">$3363$</td>
<td align="center">$533$</td>
<td align="center">$21$</td>
<td align="center">$0$</td>
<td align="center">$0$</td>
</tr>
<tr>
<td align="center">$N=10^5$</td>
<td align="center">$60794$</td>
<td align="center">$33562$</td>
<td align="center">$5345$</td>
<td align="center">$297$</td>
<td align="center">$2$</td>
<td align="center">$0$</td>
</tr>
<tr>
<td align="center">$N=10^6$</td>
<td align="center">$607926$</td>
<td align="center">$335438$</td>
<td align="center">$53358$</td>
<td align="center">$3218$</td>
<td align="center">$60$</td>
<td align="center">$0$</td>
</tr>
<tr>
<td align="center">$N=10^7$</td>
<td align="center">$6079291$</td>
<td align="center">$3353956$</td>
<td align="center">$533140$</td>
<td align="center">$32777$</td>
<td align="center">$834$</td>
<td align="center">$2$</td>
</tr>
<tr>
<td align="center">$N=10^8$</td>
<td align="center">$60792694$</td>
<td align="center">$33539196$</td>
<td align="center">$5329747$</td>
<td align="center">$329028$</td>
<td align="center">$9257$</td>
<td align="center">$78$</td>
</tr>
</tbody></table>
Find the product of all non-zero $C_k(10^{16})$. Give the result reduced modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码


