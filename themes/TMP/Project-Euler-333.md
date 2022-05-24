---
title: Project Euler 333
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 333
## 题目
### Special partitions

All positive integers can be partitioned in such a way that each and every term of the partition can be expressed as 2^ix3^j, where i,j \ge 0.

Let's consider only such partitions where none of the terms can divide any of the other terms.
<br />For example, the partition of 17 = 2 + 6 + 9 = (2^1x3^0 + 2^1x3^1 + 2^0x3^2) would not be valid since 2 can divide 6. Neither would the partition 17 = 16 + 1 = (2^4x3^0 + 2^0x3^0) since 1 can divide 16. The only valid partition of 17 would be 8 + 9 = (2^3x3^0 + 2^0x3^2).

Many integers have more than one valid partition, the first being 11 having the following two partitions.
<br />11 = 2 + 9 = (2^1x3^0 + 2^0x3^2)
<br />11 = 8 + 3 = (2^3x3^0 + 2^0x3^1)

Let's define P(<var>n</var>) as the number of valid partitions of <var>n</var>. For example, P(11) = 2.

Let's consider only the prime integers <var>q</var> which would have a single valid partition such as P(17).

The sum of the primes <var>q</var> <100 such that P(<var>q</var>)=1 equals 233.

Find the sum of the primes <var>q</var> <1000000 such that P(<var>q</var>)=1.


# Project Euler 333
## 题目
### Special partitions

All positive integers can be partitioned in such a way that each and every term of the partition can be expressed as 2^i\times3^j, where i,j \ge 0.
Let’s consider only those such partitions where none of the terms can divide any of the other terms.<br>For example, the partition of 17 = 2 + 6 + 9 = (2^1\times3^0 + 2^1\times3^1 + 2^0\times3^2) would not be valid since 2 can divide 6. Neither would the partition 17 = 16 + 1 = (2^4\times3^0 + 2^0\times3^0) since 1 can divide 16. The only valid partition of 17 would be 8 + 9 = (2^3\times3^0 + 2^0\times3^2).
Many integers have more than one valid partition, the first being 11 having the following two partitions.<br>11 = 2 + 9 = (2^1\times3^0 + 2^0\times3^2)<br>11 = 8 + 3 = (2^3\times3^0 + 2^0\times3^1)
Let’s define P(n) as the number of valid partitions of n. For example, P(11) = 2.
Let’s consider only the prime integers q which would have a single valid partition such as P(17).
The sum of the primes q <100 such that P(q)=1 equals 233.
Find the sum of the primes q <1000000 such that P(q)=1.


## 解决方案


## 代码


