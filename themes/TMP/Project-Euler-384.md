---
title: Project Euler 384
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 384
## 题目
### Rudin-Shapiro sequence

Define the sequence a(n) as the number of adjacent pairs of ones in the binary expansion of n (possibly overlapping).
<br />E.g.: a(5) = a(101_2) = 0, a(6) = a(110_2) = 1, a(7) = a(111_2) = 2

Define the sequence b(n) = (-1)^a(n).
<br />This sequence is called the <b>Rudin-Shapiro</b> sequence.
Also consider the summatory sequence of b(n): $s(n) = \sum \limits_{i = 0}^{n} {b(i)}$.

The first couple of values of these sequences are:
<br /><tt>n        0     1     2     3     4     5     6     7
<br />a(n)     0     0     0     1     0     0     1     2
<br />b(n)     1     1     1    -1     1     1    -1     1
<br />s(n)     1     2     3     2     3     4     3     4</tt>

The sequence s(n) has the remarkable property that all elements are positive and every positive integer k occurs exactly k times.

Define g(t,c), with 1 \le c \le t, as the index in s(n) for which t occurs for the c'th time in s(n).
<br />E.g.: g(3,3) = 6, g(4,2) = 7 and g(54321,12345) = 1220847710.

Let F(n) be the fibonacci sequence defined by:
<br />F(0)=F(1)=1 and
<br />F(n)=F(n-1)+F(n-2) for n>1.

Define GF(t)=g(F(t),F(t-1)).

Find $\sum$ GF(t) for 2\let\le45.


# Project Euler 384
## 题目
### Rudin-Shapiro sequence

Define the sequence a(n) as the number of adjacent pairs of ones in the binary expansion of n (possibly overlapping).<br>E.g.: a(5) = a(101_2) = 0, a(6) = a(110_2) = 1, a(7) = a(111_2) = 2
Define the sequence b(n) = (-1)^a(n).<br>This sequence is called the <b>Rudin-Shapiro</b> sequence.
Also consider the summatory sequence of b(n): $s(n)=\sum_{i=0}^{n}b(i)$.
The first couple of values of these sequences are:
<table>
<thead>
<tr>
<th align="center">n</th>
<th align="center">&nbsp;0</th>
<th align="center">&nbsp;1</th>
<th align="center">&nbsp;2</th>
<th align="center">&nbsp;3</th>
<th align="center">&nbsp;4</th>
<th align="center">&nbsp;5</th>
<th align="center">&nbsp;6</th>
<th align="center">&nbsp;7</th>
</tr>
</thead>
<tbody><tr>
<td align="center">a(n)</td>
<td align="center">&nbsp;0</td>
<td align="center">&nbsp;0</td>
<td align="center">&nbsp;0</td>
<td align="center">&nbsp;1</td>
<td align="center">&nbsp;0</td>
<td align="center">&nbsp;0</td>
<td align="center">&nbsp;1</td>
<td align="center">&nbsp;2</td>
</tr>
<tr>
<td align="center">b(n)</td>
<td align="center">&nbsp;1</td>
<td align="center">&nbsp;1</td>
<td align="center">&nbsp;1</td>
<td align="center">-1</td>
<td align="center">&nbsp;1</td>
<td align="center">&nbsp;1</td>
<td align="center">-1</td>
<td align="center">&nbsp;1</td>
</tr>
<tr>
<td align="center">s(n)</td>
<td align="center">&nbsp;1</td>
<td align="center">&nbsp;2</td>
<td align="center">&nbsp;3</td>
<td align="center">&nbsp;2</td>
<td align="center">&nbsp;3</td>
<td align="center">&nbsp;4</td>
<td align="center">&nbsp;3</td>
<td align="center">&nbsp;4</td>
</tr>
</tbody></table>
The sequence s(n) has the remarkable property that all elements are positive and every positive integer k occurs exactly k times.
Define g(t,c), with 1 \le c \le t, as the index in s(n) for which t occurs for the c’th time in s(n).<br>E.g.: g(3,3) = 6, g(4,2) = 7 and g(54321,12345) = 1220847710.
Let F(n) be the fibonacci sequence defined by:<br>F(0)=F(1)=1 and<br>F(n)=F(n-1)+F(n-2) for n>1.
Define GF(t)=g(F(t),F(t-1)).
Find \sumGF(t) for 2\let\le45.


## 解决方案


## 代码


