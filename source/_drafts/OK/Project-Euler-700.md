---
title: Project Euler 700
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 700
## 题目
### Eulercoin

Leonhard Euler was born on $15$ April $1707$.

Consider the sequence $1504170715041707n \mod 4503599627370517$.

An element of this sequence is defined to be an Eulercoin if it is strictly smaller than all previously found Eulercoins.

For example, the first term is $1504170715041707$ which is the first Eulercoin. The second term is $3008341430083414$ which is greater than $1504170715041707$ so is not an Eulercoin. However, the third term is $8912517754604$ which is small enough to be a new Eulercoin.

The sum of the first $2$ Eulercoins is therefore $1513083232796311$.

Find the sum of all Eulercoins.


## 解决方案

令$A=1504170715041707,B=4503599627370517.$

令$e_0=B,e_1=A,e_n=-e_{n-2}\%e_{n-1}$，存在一个项最终$e_m=0$，那么对于$1\le i<m$，$e_i$都是欧拉币。

## 代码


```py
A = 1504170715041707
B = 4503599627370517
ans = 0
while A > 0:
    ans += A
    A, B = -B % A, A
print(ans)

```