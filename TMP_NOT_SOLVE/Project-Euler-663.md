---
title: Project Euler 663
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 663
## 题目
### Sums of subarrays

Let $t_k$ be the <b>tribonacci numbers</b> defined as: <br />
$\quad t_0 = t_1 = 0$;<br />
$\quad t_2 = 1$; <br />
$\quad t_k = t_{k-1} + t_{k-2} + t_{k-3} \quad \text{   for   }  k \ge 3$.

For a given integer $n$, let $A_n$ be an array of length $n$ (indexed from 0 to $n-1$), that is initially filled with zeros.<br />
The array is changed iteratively by replacing $A_n[(t_{2 i-2} \text{ mod } n)]$ with $A_n[(t_{2 i-2} \text{ mod } n)]+2 (t_{2 i-1} \text{ mod } n)-n+1$ in each step $i$.<br /> 
After each step $i$, define $M_n(i)$ to be $\displaystyle \max\{\sum_{j=p}^q A_n[j]: 0\le p\le q<n\}$, the maximal sum of any contiguous subarray of $A_n$. 

The first 6 steps for $n=5$ are illustrated below:<br />
Initial state: $\, A_5=\{0,0,0,0,0\}$<br />
Step 1:   $\quad \Rightarrow A_5=\{-4,0,0,0,0\}$ , $M_5(1)=0$<br />
Step 2: $\quad \Rightarrow A_5=\{-4, -2, 0, 0, 0\}$ , $M_5(2)=0$<br />
Step 3: $\quad \Rightarrow A_5=\{-4, -2, 4, 0, 0\}$ , $M_5(3)=4$<br />
Step 4: $\quad \Rightarrow A_5=\{-4, -2, 6, 0, 0\}$ , $M_5(4)=6$<br />
Step 5: $\quad \Rightarrow A_5=\{-4, -2, 6, 0, 4\}$ , $M_5(5)=10$<br />
Step 6: $\quad \Rightarrow A_5=\{-4, 2, 6, 0, 4\}$ , $M_5(6)=12$<br />

Let $\displaystyle S(n,l)=\sum_{i=1}^l M_n(i)$. Thus $S(5,6)=32$.<br />
You are given $S(5,100)=2416$, $S(14,100)=3881$ and $S(107,1000)=1618572$.

Find $S(10\,000\,003,10\,200\,000)-S(10\,000\,003,10\,000\,000)$.


# Project Euler 663
## 题目
### Sums of subarrays

Let $t_k$ be the **tribonacci numbers** defined as:<br>$\quad t_0 = t_1 = 0$;<br>$\quad t_2 = 1$;<br>$\quad t_k = t_{k-1} + t_{k-2} + t_{k-3}$ for $k \ge 3$.
For a given integer $n$, let $A_n$ be an array of length $n$ (indexed from 0 to $n-1$), that is initially filled with zeros.<br>The array is changed iteratively by replacing $A_n[(t_{2 i-2} \text{ mod } n)]$ with $A_n[(t_{2 i-2} \text{ mod } n)]+2 (t_{2 i-1} \text{ mod } n)-n+1$ in each step $i$.<br>After each step $i$, define $M_n(i)$ to be $\displaystyle \max{\sum_{j=p}^q A_n[j]: 0\le p\le q<n}$, the maximal sum of any contiguous subarray of $A_n$. 
The first $6$ steps for $n=5$ are illustrated below:<br>Initial state: $, A_5={0,0,0,0,0}$<br>Step $1$: $\quad \Rightarrow A_5={-4,0,0,0,0}$ , $M_5(1)=0$<br>Step $2$: $\quad \Rightarrow A_5={-4, -2, 0, 0, 0}$ , $M_5(2)=0$<br>Step $3$: $\quad \Rightarrow A_5={-4, -2, 4, 0, 0}$ , $M_5(3)=4$<br>Step $4$: $\quad \Rightarrow A_5={-4, -2, 6, 0, 0}$ , $M_5(4)=6$<br>Step $5$: $\quad \Rightarrow A_5={-4, -2, 6, 0, 4}$ , $M_5(5)=10$<br>Step $6$: $\quad \Rightarrow A_5={-4, 2, 6, 0, 4}$ , $M_5(6)=12$
Let $\displaystyle S(n,l)=\sum_{i=1}^l M_n(i)$. Thus $S(5,6)=32$.<br>You are given $S(5,100)=2416$, $S(14,100)=3881$ and $S(107,1000)=1618572$.
Find $S(10,000,003,10,200,000)-S(10,000,003,10,000,000)$.


## 解决方案


## 代码


