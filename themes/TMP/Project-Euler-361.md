---
title: Project Euler 361
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 361
## 题目
### Subsequence of Thue-Morse sequence

The <b>Thue-Morse sequence</b> {T_<var>n</var>} is a binary sequence satisfying:
<ul><li>T_0 = 0</li>
<li>T_2<var>n</var> = T_<var>n</var></li>
<li>T_2<var>n</var>+1 = 1 - T_<var>n</var></li>
</ul>
The first several terms of {T_<var>n</var>} are given as follows:<br />
01101001<span style="color:#FF0000;">10010</span>1101001011001101001\dots.



We define {A_<var>n</var>} as the sorted sequence of integers such that the binary expression of each element appears as a subsequence in {T_<var>n</var>}.<br />
For example, the decimal number 18 is expressed as 10010 in binary. 10010 appears in {T_<var>n</var>} (T_8 to T_12), so 18 is an element of {A_<var>n</var>}.<br />
The decimal number 14 is expressed as 1110 in binary. 1110 never appears in {T_<var>n</var>}, so 14 is not an element of {A_<var>n</var>}.



The first several terms of A_<var>n</var> are given as follows:<br /><div align="center">
<table cellspacing="1" cellpadding="5" border="0" align="center"><tr><td align="left"><var>n</var></td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td><td>11</td><td>12</td><td>\dots</td></tr><tr><td>A_<var>n</var></td><td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td><td>6</td><td>9</td><td>10</td><td>11</td><td>12</td><td>13</td><td>18</td><td>\dots</td></tr></table></div>



We can also verify that A_100 = 3251 and A_1000 = 80852364498.



Find the last 9 digits of $\sum \limits_{k = 1}^{18} {A_{10^k}}$.



# Project Euler 361
## 题目
### Subsequence of Thue-Morse sequence

The <b>Thue-Morse sequence</b> {T_n} is a binary sequence satisfying:
<ul>
<li>T_0 = 0</li>
<li>T_2n = T_n</li>
<li>T_2n+1 = 1 - T_n</li>
</ul>
The first several terms of {T_n} are given as follows:<br>01101001<span style="color:red;">10010</span>1101001011001101001\dots.
We define {A_n} as the sorted sequence of integers such that the binary expression of each element appears as a subsequence in {T_n}.<br>For example, the decimal number 18 is expressed as 10010 in binary. 10010 appears in {T_n} (T_8 to T_12), so 18 is an element of {A_n}.<br>The decimal number 14 is expressed as 1110 in binary. 1110 never appears in {T_n}, so 14 is not an element of {A_n}.
The first several terms of A_n are given as follows:
<table>
<thead>
<tr>
<th>n</th>
<th>0&nbsp;</th>
<th>1&nbsp;</th>
<th>2&nbsp;</th>
<th>3&nbsp;</th>
<th>4&nbsp;</th>
<th>5&nbsp;</th>
<th>6&nbsp;</th>
<th>7&nbsp;</th>
<th>8&nbsp;</th>
<th>9&nbsp;</th>
<th>10</th>
<th>11</th>
<th>12</th>
<th>\dots</th>
</tr>
</thead>
<tbody><tr>
<td>$A_n$</td>
<td>0&nbsp;</td>
<td>1&nbsp;</td>
<td>2&nbsp;</td>
<td>3&nbsp;</td>
<td>4&nbsp;</td>
<td>5&nbsp;</td>
<td>6&nbsp;</td>
<td>9&nbsp;</td>
<td>10</td>
<td>11</td>
<td>12</td>
<td>13</td>
<td>18</td>
<td>\dots</td>
</tr>
</tbody></table>
We can also verify that A_100 = 3251 and A_1000 = 80852364498.
Find the last 9 digits of $\sum_{k=1}^{18}A_{10^k}$.


## 解决方案


## 代码


