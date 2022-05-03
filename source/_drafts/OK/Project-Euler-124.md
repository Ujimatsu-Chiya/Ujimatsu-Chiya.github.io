---
title: Project Euler 124
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
   

# Project Euler 124
## 题目
### Ordered radicals
The radical of $n$, $\mathrm{rad}(n)$, is the product of the distinct prime factors of $n$. For example, $504 = 2^3 × 3^2 × 7$, so $\mathrm{rad}(504) = 2 × 3 × 7 = 42$.

If we calculate $\mathrm{rad}(n)$ for $1 \le n \le 10$, then sort them on rad(n), and sorting on n if the radical values are equal, we get:

||**Unsorted**|||**Sorted**||
|-|-|-|-|-|-|
|$\mathbf{n}$|$\mathbf{rad}(n)$||$\mathbf{n}$|$\mathbf{rad}(n)$|$\mathbf{k}$|
|$1$|$1$||$1$|$1$|$1$|
|$2$|$2$||$2$|$2$|$2$|
|$3$|$3$||$4$|$2$|$3$|
|$4$|$2$||$8$|$2$|$4$|
|$5$|$5$||$3$|$3$|$5$|
|$6$|$6$||$9$|$3$|$6$|
|$7$|$7$||$5$|$5$|$7$|
|$8$|$2$||$6$|$6$|$8$|
|$9$|$3$||$7$|$7$|$9$|
|$10$|$10$||$10$|$10$|$10$|


Let $E(k)$ be the $k\mathrm{th}$ element in the sorted n column; for example, $E(4) = 8$ and $E(6) = 9$.

If $\mathrm{rad}(n)$ is sorted for $1 \le n \le 100000$, find $E(10000)$.


## 解决方案


## 代码


