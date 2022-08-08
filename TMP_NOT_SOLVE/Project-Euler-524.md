---
title: Project Euler 524
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 524
## 题目
### First Sort II


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

We can list all permutations <var>P</var> of the integers {1, 2, \dots, <var>n</var>} in <b>lexicographical order</b>, and assign to each permutation an index <var>I</var>_<var>n</var>(<var>P</var>) from 1 to <var>n</var>! corresponding to its position in the list.

Let <var>Q</var>(<var>n</var>, <var>k</var>) = min(<var>I</var>_<var>n</var>(<var>P</var>)) for <var>F</var>(<var>P</var>) = <var>k</var>, the index of the first permutation requiring exactly <var>k</var> steps to sort with First Sort. If there is no permutation for which <var>F</var>(<var>P</var>) = <var>k</var>, then <var>Q</var>(<var>n</var>, <var>k</var>) is undefined.

For <var>n</var> = 4 we have:

<table border="1" style="text-align:left;"><tr><th><var>P</var></th><th><var>I</var>_4(<var>P</var>)</th><th><var>F</var>(<var>P</var>)</th><th></th></tr><tr><td>{1, 2, 3, 4}</td><td>1</td><td>0</td><td>Q(4, 0) = 1</td></tr><tr><td>{1, 2, 4, 3}</td><td>2</td><td>4</td><td>Q(4, 4) = 2</td></tr><tr><td>{1, 3, 2, 4}</td><td>3</td><td>2</td><td>Q(4, 2) = 3</td></tr><tr><td>{1, 3, 4, 2}</td><td>4</td><td>2</td><td></td></tr><tr><td>{1, 4, 2, 3}</td><td>5</td><td>6</td><td>Q(4, 6) = 5</td></tr><tr><td>{1, 4, 3, 2}</td><td>6</td><td>4</td><td></td></tr><tr><td>{2, 1, 3, 4}</td><td>7</td><td>1</td><td>Q(4, 1) = 7</td></tr><tr><td>{2, 1, 4, 3}</td><td>8</td><td>5</td><td>Q(4, 5) = 8</td></tr><tr><td>{2, 3, 1, 4}</td><td>9</td><td>1</td><td></td></tr><tr><td>{2, 3, 4, 1}</td><td>10</td><td>1</td><td></td></tr><tr><td>{2, 4, 1, 3}</td><td>11</td><td>5</td><td></td></tr><tr><td>{2, 4, 3, 1}</td><td>12</td><td>3</td><td>Q(4, 3) = 12</td></tr><tr><td>{3, 1, 2, 4}</td><td>13</td><td>3</td><td></td></tr><tr><td>{3, 1, 4, 2}</td><td>14</td><td>3</td><td></td></tr><tr><td>{3, 2, 1, 4}</td><td>15</td><td>2</td><td></td></tr><tr><td>{3, 2, 4, 1}</td><td>16</td><td>2</td><td></td></tr><tr><td>{3, 4, 1, 2}</td><td>17</td><td>3</td><td></td></tr><tr><td>{3, 4, 2, 1}</td><td>18</td><td>2</td><td></td></tr><tr><td>{4, 1, 2, 3}</td><td>19</td><td>7</td><td>Q(4, 7) = 19</td></tr><tr><td>{4, 1, 3, 2}</td><td>20</td><td>5</td><td></td></tr><tr><td>{4, 2, 1, 3}</td><td>21</td><td>6</td><td></td></tr><tr><td>{4, 2, 3, 1}</td><td>22</td><td>4</td><td></td></tr><tr><td>{4, 3, 1, 2}</td><td>23</td><td>4</td><td></td></tr><tr><td>{4, 3, 2, 1}</td><td>24</td><td>3</td><td></td></tr></table>Let <var>R</var>(<var>k</var>) = min(<var>Q</var>(<var>n</var>, <var>k</var>)) over all <var>n</var> for which <var>Q</var>(<var>n</var>, <var>k</var>) is defined.

Find <var>R</var>(12^12).



# Project Euler 524
## 题目
### First Sort II

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
We can list all permutations P of the integers {1, 2, \dots, n} in <b>lexicographical order</b>, and assign to each permutation an index I_n(P) from 1 to n! corresponding to its position in the list.
Let Q(n, k) = min(I_n(P)) for F(P) = k, the index of the first permutation requiring exactly k steps to sort with First Sort. If there is no permutation for which F(P) = k, then Q(n, k) is undefined.
For n = 4 we have:
<table>
<thead>
<tr>
<th align="center">P</th>
<th align="center">I_4(P)</th>
<th align="center">F(P)</th>
<th align="center">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="center">{1, 2, 3, 4}</td>
<td align="center">1</td>
<td align="center">0</td>
<td align="center">Q(4, 0) = 1</td>
</tr>
<tr>
<td align="center">{1, 2, 4, 3}</td>
<td align="center">2</td>
<td align="center">4</td>
<td align="center">Q(4, 4) = 2</td>
</tr>
<tr>
<td align="center">{1, 3, 2, 4}</td>
<td align="center">3</td>
<td align="center">2</td>
<td align="center">Q(4, 2) = 3</td>
</tr>
<tr>
<td align="center">{1, 3, 4, 2}</td>
<td align="center">4</td>
<td align="center">2</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{1, 4, 2, 3}</td>
<td align="center">5</td>
<td align="center">6</td>
<td align="center">Q(4, 6) = 5</td>
</tr>
<tr>
<td align="center">{1, 4, 3, 2}</td>
<td align="center">6</td>
<td align="center">4</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{2, 1, 3, 4}</td>
<td align="center">7</td>
<td align="center">1</td>
<td align="center">Q(4, 1) = 7</td>
</tr>
<tr>
<td align="center">{2, 1, 4, 3}</td>
<td align="center">8</td>
<td align="center">5</td>
<td align="center">Q(4, 5) = 8</td>
</tr>
<tr>
<td align="center">{2, 3, 1, 4}</td>
<td align="center">9</td>
<td align="center">1</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{2, 3, 4, 1}</td>
<td align="center">10</td>
<td align="center">1</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{2, 4, 1, 3}</td>
<td align="center">11</td>
<td align="center">5</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{2, 4, 3, 1}</td>
<td align="center">12</td>
<td align="center">3</td>
<td align="center">Q(4, 3) = 12</td>
</tr>
<tr>
<td align="center">{3, 1, 2, 4}</td>
<td align="center">13</td>
<td align="center">3</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{3, 1, 4, 2}</td>
<td align="center">14</td>
<td align="center">3</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{3, 2, 1, 4}</td>
<td align="center">15</td>
<td align="center">2</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{3, 2, 4, 1}</td>
<td align="center">16</td>
<td align="center">2</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{3, 4, 1, 2}</td>
<td align="center">17</td>
<td align="center">3</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{3, 4, 2, 1}</td>
<td align="center">18</td>
<td align="center">2</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{4, 1, 2, 3}</td>
<td align="center">19</td>
<td align="center">7</td>
<td align="center">Q(4, 7) = 19</td>
</tr>
<tr>
<td align="center">{4, 1, 3, 2}</td>
<td align="center">20</td>
<td align="center">5</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{4, 2, 1, 3}</td>
<td align="center">21</td>
<td align="center">6</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{4, 2, 3, 1}</td>
<td align="center">22</td>
<td align="center">4</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{4, 3, 1, 2}</td>
<td align="center">23</td>
<td align="center">4</td>
<td align="center"></td>
</tr>
<tr>
<td align="center">{4, 3, 2, 1}</td>
<td align="center">24</td>
<td align="center">3</td>
<td align="center"></td>
</tr>
</tbody></table>
Let R(k) = min(Q(n, k)) over all n for which Q(n, k) is defined.
Find R(12^12).


## 解决方案


## 代码


