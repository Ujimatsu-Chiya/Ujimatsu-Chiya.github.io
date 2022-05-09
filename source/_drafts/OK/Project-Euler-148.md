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

[卢卡斯定理](https://en.wikipedia.org/wiki/Lucas%27s_theorem)：如果$p$是一个质数，那么计算组合数$C_n^m\% p$时可用以下公式。

$$C_n^m \equiv C_{n\%p}^{m\%p} \cdot C_{\lfloor\frac{n}{p}\rfloor}^{\lfloor\frac{m}{p}\rfloor}( \mod p)$$

其中，在计算过程中，如果发生了$m>n$，那么$C_n^m\%p=0$。

可以看成是假设有两个等长的$p$进制数（可以有前导$0$）：$a=a_{k-1}\dots a_2a_1a_0,b= b_{k-1}\dots b_2b_1b_0$。那么

$$C_a^b\equiv  C_{a_{k-1}}^{b_{k-1}}\dots C_{a_2}^{b_2}C_{a_1}^{b_1}C_{a_0}^{b_0}(\mod p) $$


## 解决方案

根据卢卡斯定理，上面的问题可以化简成如下形式

有多少对$(i,j)(0\leq j \le i <n )$，满足以下条件：

将$i$和$j$写成两个长度为$k$的$p$进制数：$i=i_{k-1}\dots i_2i_1i_0,j=j_{k-1}\dots j_2j_1j_0$。那么$\forall q:0\le q<k ,j_q\le i_q $.

根据卢卡斯定理的描述，如果有一个$j_q>i_q$，那么整个式子模$p$的值为$0$，也就是能被$p$整除。

## 代码


