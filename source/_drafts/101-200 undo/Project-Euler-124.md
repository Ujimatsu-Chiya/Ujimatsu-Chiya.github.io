---
title: Project Euler 124
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 124
## 题目
### Ordered radicals

The radical of <i>n</i>, rad(<i>n</i>), is the product of the distinct prime factors of <i>n</i>. For example, 504 = 2^3 × 3^2 × 7, so rad(504) = 2 × 3 × 7 = 42.
If we calculate rad(<i>n</i>) for <i>1</i> ≤ <i>n</i> ≤ 10, then sort them on rad(<i>n</i>), and sorting on <i>n</i> if the radical values are equal, we get:
<table class="center"><tr><th colspan="2">Unsorted</th>
   <td class="w25"> </td>
   <th colspan="3">Sorted</th>
</tr><tr><th class="w50"><i>n</i></th>
   <th class="w50">rad(<i>n</i>)</th>
   <td> </td>
   <th class="w50"><i>n</i></th>
   <th class="w50">rad(<i>n</i>)</th>
   <th class="w50">k</th>
</tr><tr><td>1</td><td>1</td>
   <td> </td>
   <td>1</td><td>1</td><td>1</td>
</tr><tr><td>2</td><td>2</td>
   <td> </td>
   <td>2</td><td>2</td><td>2</td>
</tr><tr><td>3</td><td>3</td>
   <td> </td>
   <td>4</td><td>2</td><td>3</td>
</tr><tr><td>4</td><td>2</td>
   <td> </td>
   <td>8</td><td>2</td><td>4</td>
</tr><tr><td>5</td><td>5</td>
   <td> </td>
   <td>3</td><td>3</td><td>5</td>
</tr><tr><td>6</td><td>6</td>
   <td> </td>
   <td>9</td><td>3</td><td>6</td>
</tr><tr><td>7</td><td>7</td>
   <td> </td>
   <td>5</td><td>5</td><td>7</td>
</tr><tr><td>8</td><td>2</td>
   <td> </td>
   <td>6</td><td>6</td><td>8</td>
</tr><tr><td>9</td><td>3</td>
   <td> </td>
   <td>7</td><td>7</td><td>9</td>
</tr><tr><td>10</td><td>10</td>
   <td> </td>
   <td>10</td><td>10</td><td>10</td>
</tr></table>Let E(<i>k</i>) be the <i>k</i>th element in the sorted <i>n</i> column; for example, E(4) = 8 and E(6) = 9.
If rad(<i>n</i>) is sorted for 1 ≤ <i>n</i> ≤ 100000, find E(10000).


# Project Euler 124
## 题目
### Ordered radicals
The radical of n, rad(n), is the product of the distinct prime factors of n. For example, 504 = 2^3 × 3^2 × 7, so rad(504) = 2 × 3 × 7 = 42.
If we calculate rad(n) for 1 ≤ n ≤ 10, then sort them on rad(n), and sorting on n if the radical values are equal, we get:
<table>
<thead>
<tr>
<th align="center">&nbsp;</th>
<th align="center">**Unsorted**</th>
<th align="center">&nbsp;</th>
<th align="center">&nbsp;</th>
<th align="center">**Sorted**</th>
<th align="center">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="center">**n**</td>
<td align="center">**rad(n)**</td>
<td align="center">&nbsp;</td>
<td align="center">**n**</td>
<td align="center">**rad(n)**</td>
<td align="center">**k**</td>
</tr>
<tr>
<td align="center">1</td>
<td align="center">1</td>
<td align="center">&nbsp;</td>
<td align="center">1</td>
<td align="center">1</td>
<td align="center">1</td>
</tr>
<tr>
<td align="center">2</td>
<td align="center">2</td>
<td align="center">&nbsp;</td>
<td align="center">2</td>
<td align="center">2</td>
<td align="center">2</td>
</tr>
<tr>
<td align="center">3</td>
<td align="center">3</td>
<td align="center">&nbsp;</td>
<td align="center">4</td>
<td align="center">2</td>
<td align="center">3</td>
</tr>
<tr>
<td align="center">4</td>
<td align="center">2</td>
<td align="center">&nbsp;</td>
<td align="center">8</td>
<td align="center">2</td>
<td align="center">4</td>
</tr>
<tr>
<td align="center">5</td>
<td align="center">5</td>
<td align="center">&nbsp;</td>
<td align="center">3</td>
<td align="center">3</td>
<td align="center">5</td>
</tr>
<tr>
<td align="center">6</td>
<td align="center">6</td>
<td align="center">&nbsp;</td>
<td align="center">9</td>
<td align="center">3</td>
<td align="center">6</td>
</tr>
<tr>
<td align="center">7</td>
<td align="center">7</td>
<td align="center">&nbsp;</td>
<td align="center">5</td>
<td align="center">5</td>
<td align="center">7</td>
</tr>
<tr>
<td align="center">8</td>
<td align="center">2</td>
<td align="center">&nbsp;</td>
<td align="center">6</td>
<td align="center">6</td>
<td align="center">8</td>
</tr>
<tr>
<td align="center">9</td>
<td align="center">3</td>
<td align="center">&nbsp;</td>
<td align="center">7</td>
<td align="center">7</td>
<td align="center">9</td>
</tr>
<tr>
<td align="center">10</td>
<td align="center">10</td>
<td align="center">&nbsp;</td>
<td align="center">10</td>
<td align="center">10</td>
<td align="center">10</td>
</tr>
</tbody></table>
Let E(k) be the kth element in the sorted n column; for example, E(4) = 8 and E(6) = 9.
If rad(n) is sorted for 1 ≤ n ≤ 100000, find E(10000).


## 解决方案


## 代码


