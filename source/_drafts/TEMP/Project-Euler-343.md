---
title: Project Euler 343
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 343
## 题目
### Fractional Sequences


For any positive integer <var>k</var>, a finite sequence a_<var>i</var> of fractions x_<var>i</var>/y_<var>i</var> is defined by:<br />
a_1 = 1/<var>k</var> and<br />
a_<var>i</var> = (x_<var>i</var>-1+1)/(y_<var>i</var>-1-1) reduced to lowest terms for <var>i</var>>1.<br />
When a_<var>i</var> reaches some integer <var>n</var>, the sequence stops. (That is, when y_<var>i</var>=1.)<br />
Define f(<var>k</var>) = <var>n</var>. <br />
For example, for <var>k</var> = 20:



1/20 → 2/19 → 3/18 = 1/6 → 2/5 → 3/4 → 4/3 → 5/2 → 6/1 = 6



So f(20) = 6.



Also f(1) = 1, f(2) = 2, f(3) = 1 and <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(<var>k</var>^3) = 118937 for 1 \le <var>k</var> \le 100.



Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(<var>k</var>^3) for 1 \le <var>k</var> \le 2\times10^6.



# Project Euler 343
## 题目
### Fractional Sequences

For any positive integer $k$, a finite sequence $a_i$ of fractions $x_i/y_i$ is defined by:

$a_1 = 1/k$ and<br>
$a_i = (x_i-1+1)/(y_i-1-1)$ reduced to lowest terms for i>1.<br>When a_i reaches some integer n, the sequence stops. (That is, when y_i=1.)<br>Define f(k) = n.<br>For example, for k = 20:
1/20 → 2/19 → 3/18 = 1/6 → 2/5 → 3/4 → 4/3 → 5/2 → 6/1 = 6
So f(20) = 6.
Also f(1) = 1, f(2) = 2, f(3) = 1 and \sumf(k^3) = 118937 for 1 \le k \le 100.
Find \sumf(k^3) for 1 \le k \le 2\times10^6.


## 解决方案


## 代码


