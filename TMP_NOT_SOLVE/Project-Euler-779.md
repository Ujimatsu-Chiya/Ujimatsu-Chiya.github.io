---
title: Project Euler 779
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 779
## 题目
### Prime Factor and Exponent


For a positive integer $n>1$, let $p(n)$ be the smallest prime dividing $n$, and let $\alpha(n)$ be its <b><i>p</i>-adic order</b>, i.e. the largest integer such that $p(n)^{\alpha(n)}$ divides $n$.


For a positive integer $K$, define the function $f_K(n)$ by:

<center>
$\displaystyle f_K(n)=\frac{\alpha(n)-1}{(p(n))^K}$
</center>

Also define $\overline{f_K}$ by:

<center>
$\displaystyle \overline{f_K}=\lim_{N \to \infty} \frac{1}{N}\sum_{n=2}^{N} f_K(n)$
</center>

It can be verified that $\overline{f_1} \approx 0.282419756159$.


Find $\displaystyle \sum_{K=1}^{\infty}\overline{f_K}$. Give your answer rounded to $12$ digits after the decimal point.




## 解决方案


## 代码


