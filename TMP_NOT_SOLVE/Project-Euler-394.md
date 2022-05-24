---
title: Project Euler 394
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 394
## 题目
### Eating pie


Jeff eats a pie in an unusual way.<br />
The pie is circular. He starts with slicing an initial cut in the pie along a radius.<br />
While there is at least a given fraction <var>F</var> of pie left, he performs the following procedure:<br />
- He makes two slices from the pie centre to any point of what is remaining of the pie border, any point on the remaining pie border equally likely. This will divide the remaining pie into three pieces.<br /> 
- Going counterclockwise from the initial cut, he takes the first two pie pieces and eats them.<br />
When less than a fraction <var>F</var> of pie remains, he does not repeat this procedure. Instead, he eats all of the remaining pie.

<p align="center">
<img src="project/images/p394_eatpie.gif" alt="p394_eatpie.gif" />



For <var>x</var> \ge 1, let E(<var>x</var>) be the expected number of times Jeff repeats the procedure above with <var>F</var> = ^1/_<var>x</var>.<br />
It can be verified that  E(1) = 1, E(2) ≈ 1.2676536759, and E(7.5) ≈ 2.1215732071.


Find E(40) rounded to 10 decimal places behind the decimal point.





# Project Euler 394
## 题目
### Eating pie

Jeff eats a pie in an unusual way.<br>The pie is circular. He starts with slicing an initial cut in the pie along a radius.<br>While there is at least a given fraction F of pie left, he performs the following procedure:
<ul>
<li>He makes two slices from the pie centre to any point of what is remaining of the pie border, any point on the remaining pie border equally likely. This will divide the remaining pie into three pieces. </li>
<li>Going counterclockwise from the initial cut, he takes the first two pie pieces and eats them.<br>When less than a fraction F of pie remains, he does not repeat this procedure. Instead, he eats all of the remaining pie.</li>
</ul>
<center><img src="https://projecteuler.net/project/images/p394_eatpie.gif"></center>

For x \ge 1, let E(x) be the expected number of times Jeff repeats the procedure above with F = ^1/_x.<br>It can be verified that  E(1) = 1, E(2) ≈ 1.2676536759, and E(7.5) ≈ 2.1215732071.
Find E(40) rounded to 10 decimal places behind the decimal point.


## 解决方案


## 代码


