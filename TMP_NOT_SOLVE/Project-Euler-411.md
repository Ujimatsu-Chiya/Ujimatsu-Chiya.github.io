---
title: Project Euler 411
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 411
## 题目
### Uphill paths



Let <var>n</var> be a positive integer. Suppose there are stations at the coordinates (<var>x</var>, <var>y</var>) = (2^<var>i</var> mod <var>n</var>, 3^<var>i</var> mod <var>n</var>) for 0 \le <var>i</var> \le 2<var>n</var>. We will consider stations with the same coordinates as the same station.

We wish to form a path from (0, 0) to (<var>n</var>, <var>n</var>) such that the x and y coordinates never decrease.<br />
Let S(<var>n</var>) be the maximum number of stations such a path can pass through.

For example, if <var>n</var> = 22, there are 11 distinct stations, and a valid path can pass through at most 5 stations. Therefore, S(22) = 5.
The case is illustrated below, with an example of an optimal path:

<p align="center"><img src="project/images/p411_longpath.png" alt="p411_longpath.png" />

It can also be verified that S(123) = 14 and S(10000) = 48.

Find <span style="font-size:larger;"><span style="font-size:larger;">\sum</span></span> S(<var>k</var>^5) for 1 \le <var>k</var> \le 30.



# Project Euler 411
## 题目
### Uphill paths

Let n be a positive integer. Suppose there are stations at the coordinates (x, y) = (2^i mod n, 3^i mod n) for 0 \le i \le 2n. We will consider stations with the same coordinates as the same station.
We wish to form a path from (0, 0) to (n, n) such that the x and y coordinates never decrease.<br>Let S(n) be the maximum number of stations such a path can pass through.
For example, if n = 22, there are 11 distinct stations, and a valid path can pass through at most 5 stations. Therefore, S(22) = 5. The case is illustrated below, with an example of an optimal path:
<center><img src="https://projecteuler.net/project/images/p411_longpath.png"></center>

It can also be verified that S(123) = 14 and S(10000) = 48.
Find \sum S(k^5) for 1 \le k \le 30.


## 解决方案


## 代码


