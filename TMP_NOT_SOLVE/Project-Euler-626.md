---
title: Project Euler 626
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 626
## 题目
### Counting Binary Matrices


A binary matrix is a matrix consisting entirely of 0s and 1s. Consider the following transformations that can be performed on a binary matrix:

<ul><li>Swap any two rows</li>
<li>Swap any two columns</li>
<li>Flip all elements in a single row (1s become 0s, 0s become 1s)</li>
<li>Flip all elements in a single column</li>
</ul>Two binary matrices $A$ and $B$ will be considered <i>equivalent</i> if there is a sequence of such transformations that when applied to $A$ yields $B$. For example, the following two matrices are equivalent:
$A=\begin{pmatrix} 
  1 &amp; 0 &amp; 1 \\ 
  0 &amp; 0 &amp; 1 \\
  0 &amp; 0 &amp; 0 \\
\end{pmatrix} \quad B=\begin{pmatrix} 
  0 &amp; 0 &amp; 0 \\ 
  1 &amp; 0 &amp; 0 \\
  0 &amp; 0 &amp; 1 \\
\end{pmatrix}$
via the sequence of two transformations "Flip all elements in column 3" followed by "Swap rows 1 and 2".

Define $c(n)$ to be the maximum number of $n\times n$ binary matrices that can be found such that no two are equivalent. For example, $c(3)=3$. You are also given that $c(5)=39$ and $c(8)=656108$.

Find $c(20)$, and give your answer modulo $1\,001\,001\,011$.



# Project Euler 626
## 题目
### Counting Binary Matrices

A binary matrix is a matrix consisting entirely of 0s and 1s. Consider the following transformations that can be performed on a binary matrix:
<ul>
<li>Swap any two rows</li>
<li>Swap any two columns</li>
<li>Flip all elements in a single row (1s become 0s, 0s become 1s)</li>
<li>Flip all elements in a single column</li>
</ul>
Two binary matrices $A$ and $B$ will be considered <i>equivalent</i> if there is a sequence of such transformations that when applied to $A$ yields $B$. For example, the following two matrices are equivalent:
$$A=\begin{pmatrix}<br>1 &amp; 0 &amp; 1 \<br>0 &amp; 0 &amp; 1 \<br>0 &amp; 0 &amp; 0<br>\end{pmatrix}\quad<br>B=\begin{pmatrix}<br>0 &amp; 0 &amp; 0 \<br>1 &amp; 0 &amp; 0 \<br>0 &amp; 0 &amp; 1<br>\end{pmatrix}$$ 
via the sequence of two transformations “Flip all elements in column 3” followed by “Swap rows 1 and 2”.
Define $c(n)$ to be the maximum number of $n\times n$ binary matrices that can be found such that no two are equivalent. For example, $c(3)=3$. You are also given that $c(5)=39$ and $c(8)=656108$.
Find $c(20)$, and give your answer modulo $1\ 001\ 001\ 011$.


## 解决方案


## 代码


