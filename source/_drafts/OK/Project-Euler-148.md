---
title: Project Euler 148
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 148
## 题目
### Exploring Pascal’s triangle
We can easily verify that none of the entries in the first seven rows of Pascal’s triangle are divisible by $7$:

||||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|-|-|
|||||||1|||||||
||||||1||1||||||
|||||1||2||1|||||
||||1||3||3||1||||
|||1||4||6||4||1|||
||1||5||10||10||5||1||
|1||6||15||20||15||6||1|

However, if we check the first one hundred rows, we will find that only $2361$ of the $5050$ entries are not divisible by $7$.

Find the number of entries which are not divisible by $7$ in the first one billion ($10^9$) rows of Pascal’s triangle.

## 卢卡斯定理

卢卡斯定理：如果$p$是一个质数，那么计算组合数$C_n^m\% p$时可用以下公式。

$$C_n^m \equiv C_{n\%p}^{m\%p} \cdot C_{\lfloor\frac{n}{p}\rfloor}^{\lfloor\frac{m}{p}\rfloor}( \mod p)$$

其中，在计算过程中，如果发生了$m>n$，那么$C_n^m\%p=0$。
## 解决方案


## 代码


