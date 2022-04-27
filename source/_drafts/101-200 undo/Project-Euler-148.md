---
title: Project Euler 148
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 148
## 题目
### Exploring Pascal's triangle

We can easily verify that none of the entries in the first seven rows of Pascal's triangle are divisible by 7:
<table cellpadding="0" cellspacing="0" border="0" align="center"><tr><td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> 1</td>
</tr><tr><td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> 1</td>
<td> </td>
<td> 1</td>
</tr><tr><td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> 1</td>
<td> </td>
<td> 2</td>
<td> </td>
<td> 1</td>
</tr><tr><td> </td>
<td> </td>
<td> </td>
<td> 1</td>
<td> </td>
<td> 3</td>
<td> </td>
<td> 3</td>
<td> </td>
<td> 1</td>
</tr><tr><td> </td>
<td> </td>
<td> 1</td>
<td> </td>
<td> 4</td>
<td> </td>
<td> 6</td>
<td> </td>
<td> 4</td>
<td> </td>
<td> 1</td>
</tr><tr><td> </td>
<td> 1</td>
<td> </td>
<td> 5</td>
<td> </td>
<td>10</td>
<td> </td>
<td>10</td>
<td> </td>
<td> 5</td>
<td> </td>
<td> 1</td>
</tr><tr><td>1</td>
<td> </td>
<td> 6</td>
<td> </td>
<td>15</td>
<td> </td>
<td>20</td>
<td> </td>
<td>15</td>
<td> </td>
<td> 6</td>
<td> </td>
<td> 1</td>
</tr></table>However, if we check the first one hundred rows, we will find that only 2361 of the 5050 entries are <i>not</i> divisible by 7.

Find the number of entries which are <i>not</i> divisible by 7 in the first one billion (10^9) rows of Pascal's triangle.


# Project Euler 148
## 题目
### Exploring Pascal’s triangle
We can easily verify that none of the entries in the first seven rows of Pascal’s triangle are divisible by 7:
<table>
<thead>
<tr>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
</tr>
<tr>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
</tr>
<tr>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">2</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
</tr>
<tr>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">3</td>
<td align="center">&nbsp;</td>
<td align="center">3</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
</tr>
<tr>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">4</td>
<td align="center">&nbsp;</td>
<td align="center">6</td>
<td align="center">&nbsp;</td>
<td align="center">4</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;</td>
</tr>
<tr>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;1&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;5&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">10</td>
<td align="center">&nbsp;</td>
<td align="center">10</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;5&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;1&nbsp;</td>
<td align="center">&nbsp;</td>
</tr>
<tr>
<td align="center">&nbsp;1&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;6&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">15</td>
<td align="center">&nbsp;</td>
<td align="center">20</td>
<td align="center">&nbsp;</td>
<td align="center">15</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;6&nbsp;</td>
<td align="center">&nbsp;</td>
<td align="center">&nbsp;1&nbsp;</td>
</tr>
</tbody></table>
However, if we check the first one hundred rows, we will find that only 2361 of the 5050 entries are not divisible by 7.
Find the number of entries which are not divisible by 7 in the first one billion (10^9) rows of Pascal’s triangle.


## 解决方案


## 代码


