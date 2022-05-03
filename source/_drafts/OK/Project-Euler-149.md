---
title: Project Euler 149
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 149
## 题目
### Searching for a maximum-sum subsequence


Looking at the table below, it is easy to verify that the maximum possible sum of adjacent numbers in any direction (horizontal, vertical, diagonal or anti-diagonal) <span style="white-space:nowrap;">is 16 (= 8 + 7 + 1).</span>

<div class="center">
<table border="1" cellpadding="6" cellspacing="0" style="margin:auto;"><tbody align="right"><tr><td>−2</td><td>5</td><td>3</td><td>2</td></tr><tr><td>9</td><td>−6</td><td>5</td><td>1</td></tr><tr><td>3</td><td>2</td><td>7</td><td>3</td></tr><tr><td>−1</td><td>8</td><td>−4</td><td>  8</td></tr></tbody></table>

# Project Euler 149
## 题目
### Searching for a maximum-sum subsequence
Looking at the table below, it is easy to verify that the maximum possible sum of adjacent numbers in any direction (horizontal, vertical, diagonal or anti-diagonal) is $16 (= 8 + 7 + 1)$.

|||||
|-|-|-|-|
|$-2$|$5$|$3$|$2$|
|$9$|$-6$|$5$|$1$|
|$3$|$2$|$7$|$3$|
|$-1$|$8$|$-4$|$8$|

Now, let us repeat the search, but on a much larger scale:

First, generate four million pseudo-random numbers using a specific form of what is known as a “Lagged Fibonacci Generator”:

For $1 \leq k \leq 55, s_k = [100003 - 200003k + 300007k^3] (\mathrm{modulo\ } 1000000) - 500000$

For $56 \leq k \leq 4000000$, $s_k = [s_{k-24} + s_{k-55} + 1000000] (\mathrm{modulo\ } 1000000) - 500000$.

Thus, $s_{10} = -393027$ and $s_{100} = 86613$.

The terms of $s$ are then arranged in a $2000\times2000$ table, using the first $2000$ numbers to fill the first row (sequentially), the next $2000$ numbers to fill the second row, and so on.

Finally, find the greatest sum of (any number of) adjacent entries in any direction (horizontal, vertical, diagonal or anti-diagonal).


## 解决方案


## 代码


