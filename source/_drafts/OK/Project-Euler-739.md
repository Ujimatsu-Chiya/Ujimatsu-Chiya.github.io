---
title: Project Euler 739
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 739
## 题目
### Summation of Summations



Take a sequence of length $n$. Discard the first term then make a sequence of the partial summations. Continue to do this over and over until we are left with a single term. We define this to be $f(n)$.


Consider the example where we start with a sequence of length $8$:


$
\begin{array}{rrrrrrrr}
1&1&1&1&1&1&1&1\\
 &1&2&3&4&5& 6 &7\\
 & &2&5&9&14&20&27\\
 & & &5&14&28&48&75\\
 & & & &14&42&90&165\\
 & & & & & 42 & 132 & 297\\
 & & & & & & 132 &429\\
 & & & & & & &429\\
\end{array}
$


Then the final number is $429$, so $f(8) = 429$.


For this problem we start with the sequence $1,3,4,7,11,18,29,47,\ldots$

This is the Lucas sequence where two terms are added to get the next term.

Applying the same process as above we get $f(8) = 2663$.

You are also given $f(20) = 742296999 $ modulo $1\,000\,000\,007$

Find $f(10^8)$. Give your answer modulo $1\,000\,000\,007$.



# Project Euler 739
## 题目
### Summation of Summations

Take a sequence of length $n$. Discard the first term then make a sequence of the partial summations. Continue to do this over and over until we are left with a single term. We define this to be $f(n)$.
Consider the example where we start with a sequence of length $8$:
$$<br>\begin{array}{rrrrrrrr}<br>1 &amp; 1 &amp; 1 &amp; 1 &amp; 1 &amp; 1 &amp; 1 &amp; 1\<br>  &amp; 1 &amp; 2 &amp; 3 &amp; 4 &amp; 5 &amp;  6  &amp; 7\<br>  &amp;   &amp; 2 &amp; 5 &amp; 9 &amp; 14 &amp; 20 &amp; 27\<br>  &amp;   &amp;   &amp; 5 &amp; 14 &amp; 28 &amp; 48 &amp; 75\<br>  &amp;   &amp;   &amp;   &amp; 14 &amp; 42 &amp; 90 &amp; 165\<br>  &amp;   &amp;   &amp;   &amp;   &amp;  42  &amp;  132  &amp;  297\<br>  &amp;   &amp;   &amp;   &amp;   &amp;   &amp;  132  &amp; 429\<br>  &amp;   &amp;   &amp;   &amp;   &amp;   &amp;   &amp; 429\<br>\end{array}<br>$$
Then the final number is $429$, so $f(8) = 429$.
For this problem we start with the sequence $1,3,4,7,11,18,29,47,\ldots$<br>This is the Lucas sequence where two terms are added to get the next term.<br>Applying the same process as above we get $f(8) = 2663$.<br>You are also given $f(20) \equiv 742296999 \bmod 1\ 000\ 000\ 007$.
Find $f(10^8)$. Give your answer modulo $1\ 000\ 000\ 007$.


## 解决方案


## 代码


