---
title: Project Euler 514
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 514
## 题目
### Geoboard Shapes

A <b>geoboard</b> (of order <var>N</var>) is a square board with equally-spaced pins protruding from the surface, representing an integer point lattice for coordinates 0 \le <var>x</var>,<var>y</var> \le <var>N</var>.

John begins with a pinless geoboard. Each position on the board is a hole that can be filled with a pin. John decides to generate a random integer between 1 and <var>N</var>+1 (inclusive) for each hole in the geoboard. If the random integer is equal to 1 for a given hole, then a pin is placed in that hole.

After John is finished generating numbers for all (<var>N</var>+1)^2 holes and placing any/all corresponding pins, he wraps a tight rubberband around the entire group of pins protruding from the board. Let <var>S</var> represent the shape that is formed. <var>S</var> can also be defined as the smallest convex shape that contains all the pins.

<div align="center"><img src="project/images/p514_geoboard.png" alt="p514_geoboard.png" /></div>

The above image depicts a sample layout for <var>N</var> = 4. The green markers indicate positions where pins have been placed, and the blue lines collectively represent the rubberband. For this particular arrangement, <var>S</var> has an area of 6. If there are fewer than three pins on the board (or if all pins are collinear), <var>S</var> can be assumed to have zero area.

Let E(<var>N</var>) be the expected area of <var>S</var> given a geoboard of order <var>N</var>. For example, E(1) = 0.18750, E(2) = 0.94335, and E(10) = 55.03013 when rounded to five decimal places each.

Calculate E(100) rounded to five decimal places.


# Project Euler 514
## 题目
### Geoboard Shapes

A **geoboard** (of order N) is a square board with equally-spaced pins protruding from the surface, representing an integer point lattice for coordinates 0 \le x,y \le N.
John begins with a pinless geoboard. Each position on the board is a hole that can be filled with a pin. John decides to generate a random number between 1 and N+1 (inclusive) for each hole in the geoboard. If the random number is equal to 1 for a given hole, then a pin is placed in that hole.
After John is finished generating numbers for all (N+1)^2 holes and placing any/all corresponding pins, he wraps a tight rubberband around the entire group of pins protruding from the board. Let S represent the shape that is formed. S can also be defined as the smallest convex shape that contains all the pins.
<center><img src="https://projecteuler.net/project/images/p514_geoboard.png"></center>

The above image depicts a sample layout for N = 4. The green markers indicate positions where pins have been placed, and the blue lines collectively represent the rubberband. For this particular arrangement, S has an area of 6. If there are fewer than three pins on the board (or if all pins are collinear), S can be assumed to have zero area.
Let E(N) be the expected area of S given a geoboard of order N. For example, E(1) = 0.18750, E(2) = 0.94335, and E(10) = 55.03013 when rounded to five decimal places each.
Calculate E(100) rounded to five decimal places.


## 解决方案


## 代码


