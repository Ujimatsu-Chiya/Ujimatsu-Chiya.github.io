---
title: Project Euler 523
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 523
## 题目
### First Sort I

Consider the following algorithm for sorting a list:
<ul style="list-style-type:none;"><li>1. Starting from the beginning of the list, check each pair of adjacent elements in turn.</li>
<li>2. If the elements are out of order:
<ul style="list-style-type:none;"><li>a. Move the smallest element of the pair at the beginning of the list.</li>
<li>b. Restart the process from step 1.</li></ul></li>
<li>3. If all pairs are in order, stop.</li></ul>For example, the list { 4 1 3 2 } is sorted as follows:
<ul style="list-style-type:none;"><li><u>4 1</u> 3 2  (4 and 1 are out of order so move 1 to the front of the list)</li>
<li>1 <u>4 3</u> 2  (4 and 3 are out of order so move 3 to the front of the list)</li>
<li><u>3 1</u> 4 2  (3 and 1 are out of order so move 1 to the front of the list)</li>
<li>1 3 <u>4 2</u>  (4 and 2 are out of order so move 2 to the front of the list)</li>
<li><u>2 1</u> 3 4  (2 and 1 are out of order so move 1 to the front of the list)</li>
<li>1 2 3 4  (The list is now sorted)</li></ul>Let <var>F</var>(<var>L</var>) be the number of times step 2a is executed to sort list <var>L</var>. For example, <var>F</var>({ 4 1 3 2 }) = 5.

Let <var>E</var>(<var>n</var>) be the <b>expected value</b> of <var>F</var>(<var>P</var>) over all permutations <var>P</var> of the integers {1, 2, \dots, <var>n</var>}.<br />
You are given <var>E</var>(4) = 3.25 and <var>E</var>(10) = 115.725.

Find <var>E</var>(30). Give your answer rounded to two digits after the decimal point.


# Project Euler 523
## 题目
### First Sort I

Consider the following algorithm for sorting a list:
<ol>
<li>Starting from the beginning of the list, check each pair of adjacent elements in turn.</li>
<li>If the elements are out of order:<ul>
<li>Move the smallest element of the pair at the beginning of the list.</li>
<li>Restart the process from step 1.</li>
</ul>
</li>
<li>If all pairs are in order, stop.</li>
</ol>
For example, the list { 4 1 3 2 } is sorted as follows:
<ul>
<li><u>4 1</u> 3 2  (4 and 1 are out of order so move 1 to the front of the list)</li>
<li>1 <u>4 3</u> 2  (4 and 3 are out of order so move 3 to the front of the list)</li>
<li><u>3 1</u> 4 2  (3 and 1 are out of order so move 1 to the front of the list)</li>
<li>1 3 <u>4 2</u>  (4 and 2 are out of order so move 2 to the front of the list)</li>
<li><u>2 1</u> 3 4  (2 and 1 are out of order so move 1 to the front of the list)</li>
<li>1 2 3 4  (The list is now sorted)</li>
</ul>
Let F(L) be the number of times step 2a is executed to sort list L. For example, F({ 4 1 3 2 }) = 5.
Let E(n) be the <b>expected value</b> of F(P) over all permutations P of the integers {1, 2, \dots, n}.<br>You are given E(4) = 3.25 and E(10) = 115.725.
Find E(30). Give your answer rounded to two digits after the decimal point.


## 解决方案


## 代码


