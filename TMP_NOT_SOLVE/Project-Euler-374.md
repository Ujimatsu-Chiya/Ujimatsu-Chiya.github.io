---
title: Project Euler 374
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 374
## 题目
### Maximum Integer Partition Product

An integer partition of a number <var>n</var> is a way of writing <var>n</var> as a sum of positive integers.

Partitions that differ only in the order of their summands are considered the same.
A partition of <var>n</var> into <b>distinct parts</b> is a partition of <var>n</var> in which every part occurs at most once.

The partitions of 5 into distinct parts are:
<br />5, 4+1 and 3+2.

Let f(<var>n</var>) be the maximum product of the parts of any such partition of <var>n</var> into distinct parts and let m(<var>n</var>) be the number of elements of any such partition of <var>n</var> with that product.

So f(5)=6 and m(5)=2.

For <var>n</var>=10 the partition with the largest product is 10=2+3+5, which gives f(10)=30 and m(10)=3.
<br />And their product, f(10)·m(10) = 30·3 = 90

It can be verified that
<br /><span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(<var>n</var>)·m(<var>n</var>) for 1 \le <var>n</var> \le 100 = 1683550844462.

Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> f(<var>n</var>)·m(<var>n</var>) for 1 \le <var>n</var> \le 10^14.
<br />Give your answer modulo 982451653, the 50 millionth prime.



# Project Euler 374
## 题目
### Maximum Integer Partition Product

An integer partition of a number n is a way of writing n as a sum of positive integers.
Partitions that differ only in the order of their summands are considered the same. A partition of n into <b>distinct parts</b> is a partition of n in which every part occurs at most once.
The partitions of 5 into distinct parts are:<br>5, 4+1 and 3+2.
Let f(n) be the maximum product of the parts of any such partition of n into distinct parts and let m(n) be the number of elements of any such partition of n with that product.
So f(5)=6 and m(5)=2.
For n=10 the partition with the largest product is 10=2+3+5, which gives f(10)=30 and m(10)=3.<br>And their product, f(10)·m(10) = 30·3 = 90
It can be verified that<br>\sumf(n)·m(n) for 1 \le n \le 100 = 1683550844462.
Find \sumf(n)·m(n) for 1 \le n \le 10^14.<br>Give your answer modulo 982451653, the 50 millionth prime.


## 解决方案


## 代码


