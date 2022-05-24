---
title: Project Euler 253
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 253
## 题目
### Tidying up

A small child has a “number caterpillar” consisting of forty jigsaw pieces, each with one number on it, which, when connected together in a line, reveal the numbers 1 to 40 in order.

Every night, the child's father has to pick up the pieces of the caterpillar that have been scattered across the play room. He picks up the pieces at random and places them in the correct order.<br /> As the caterpillar is built up in this way, it forms distinct segments that gradually merge together.<br /> The number of segments starts at zero (no pieces placed), generally increases up to about eleven or twelve, then tends to drop again before finishing at a single segment (all pieces placed).

For example:
<div class="center">
<table class="grid" style="margin:0 auto;"><tr><th width="80" align="center"><b>Piece Placed</b></th>
<th width="80" align="center"><b>Segments So Far</b></th></tr><tr><td align="center">12</td><td align="center">1</td></tr><tr><td align="center">4</td><td align="center">2</td></tr><tr><td align="center">29</td><td align="center">3</td></tr><tr><td align="center">6</td><td align="center">4</td></tr><tr><td align="center">34</td><td align="center">5</td></tr><tr><td align="center">5</td><td align="center">4</td></tr><tr><td align="center">35</td><td align="center">4</td></tr><tr><td align="center">\dots</td><td align="center">\dots</td></tr></table></div>

Let <var>M</var> be the maximum number of segments encountered during a random tidy-up of the caterpillar.<br />
For a caterpillar of ten pieces, the number of possibilities for each <var>M</var> is
<div class="center">
<table class="grid" style="margin:0 auto;"><tr><th width="50" align="center"><b><var>M</var></b></th>
<th width="90" align="center"><b>Possibilities</b></th></tr><tr><td align="center">1</td><td align="right">512      </td></tr><tr><td align="center">2</td><td align="right">250912      </td></tr><tr><td align="center">3</td><td align="right">1815264      </td></tr><tr><td align="center">4</td><td align="right">1418112      </td></tr><tr><td align="center">5</td><td align="right">144000      </td></tr></table></div>

so the most likely value of <var>M</var> is 3 and the average value is ^385643⁄_113400 = 3.400732, rounded to six decimal places.

The most likely value of <var>M</var> for a forty-piece caterpillar is 11; but what is the average value of <var>M</var>?
Give your answer rounded to six decimal places.



# Project Euler 253
## 题目
### Tidying up

A small child has a “number caterpillar” consisting of forty jigsaw pieces, each with one number on it, which, when connected together in a line, reveal the numbers 1 to 40 in order.
Every night, the child’s father has to pick up the pieces of the caterpillar that have been scattered across the play room. He picks up the pieces at random and places them in the correct order. As the caterpillar is built up in this way, it forms distinct segments that gradually merge together. The number of segments starts at zero (no pieces placed), generally increases up to about eleven or twelve, then tends to drop again before finishing at a single segment (all pieces placed).
For example:
<table>
<thead>
<tr>
<th align="center">**Piece Placed**</th>
<th align="center">**Segments So Far**</th>
</tr>
</thead>
<tbody><tr>
<td align="center">12</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">4</td>
<td align="center">2</td>
</tr>
<tr>
<td align="center">29</td>
<td align="center">3</td>
</tr>
<tr>
<td align="center">6</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">34</td>
<td align="center">5</td>
</tr>
<tr>
<td align="center">5</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">35</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">\dots</td>
<td align="center">\dots</td>
</tr>
</tbody></table>
Let M be the maximum number of segments encountered during a random tidy-up of the caterpillar.<br>For a caterpillar of ten pieces, the number of possibilities for each M is
<table>
<thead>
<tr>
<th align="center">**M**</th>
<th align="center">**Possibilities**</th>
</tr>
</thead>
<tbody><tr>
<td align="center">1</td>
<td align="center">512</td>
</tr>
<tr>
<td align="center">2</td>
<td align="center">250912</td>
</tr>
<tr>
<td align="center">3</td>
<td align="center">1815264</td>
</tr>
<tr>
<td align="center">4</td>
<td align="center">1418112</td>
</tr>
<tr>
<td align="center">5</td>
<td align="center">144000</td>
</tr>
</tbody></table>
so the most likely value of M is 3 and the average value is ^385643⁄_113400 = 3.400732, rounded to six decimal places.
The most likely value of M for a forty-piece caterpillar is 11; but what is the average value of M?
Give your answer rounded to six decimal places.


## 解决方案


## 代码


