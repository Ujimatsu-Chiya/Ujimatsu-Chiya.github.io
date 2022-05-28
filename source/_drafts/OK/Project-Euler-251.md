---
title: Project Euler 251
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    



# Project Euler 251
## 题目
### Cardano Triplets

A triplet of positive integers $(a,b,c)$ is called a Cardano Triplet if it satisfies the condition:

$$\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}} = 1$$

For example, $(2,1,5)$ is a Cardano Triplet.

There exist $149$ Cardano Triplets for which $a+b+c \le 1000$.

Find how many Cardano Triplets exist such that $a+b+c \le 110,000,000$.


## 解决方案

先将整个方程去除根号：

1. 等式两边立方，整理后得

$$2a+3\sqrt[3]{a^2-b^2c}\cdot(\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}})=1$$

2. 代入原来的$\sqrt[3]{a + b \sqrt{c}} + \sqrt[3]{a - b \sqrt{c}}=1$，移项后，整理得：

$$2a-1=-3\sqrt[3]{a^2-b^2c}$$

3.等式两边再取立方，整理后得：

$$8a^3+15a^2+6a-1=27b^2c$$

原式等价于求$8a^3+15a^2+6a-1=27b^2c$的解。


## 代码


