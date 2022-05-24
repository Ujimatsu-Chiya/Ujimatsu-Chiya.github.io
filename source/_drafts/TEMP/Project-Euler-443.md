---
title: Project Euler 443
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 443
## 题目
### GCD sequence

Let g(<var>n</var>) be a sequence defined as follows:<br />
g(4) = 13,<br />
g(<var>n</var>) = g(<var>n</var>-1) + gcd(<var>n</var>, g(<var>n</var>-1)) for <var>n</var> > 4.

The first few values are:
<div align="center">
    <table cellspacing="1" cellpadding="5" border="0" align="center"><tr><td><var>n</var></td><td>4</td><td>5</td><td>6</td><td>7</td><td>8</td><td>9</td><td>10</td><td>11</td><td>12</td><td>13</td><td>14</td><td>15</td><td>16</td><td>17</td><td>18</td><td>19</td><td>20</td><td>\dots</td>
    </tr><tr><td>g(<var>n</var>)</td><td>13</td><td>14</td><td>16</td><td>17</td><td>18</td><td>27</td><td>28</td><td>29</td><td>30</td><td>31</td><td>32</td><td>33</td><td>34</td><td>51</td><td>54</td><td>55</td><td>60</td><td>\dots</td>
    </tr></table></div>

You are given that g(1 000) = 2524 and g(1 000 000) = 2624152.

Find g(10^15).


# Project Euler 443
## 题目
### GCD sequence

Let g(n) be a sequence defined as follows:<br>g(4) = 13,<br>g(n) = g(n-1) + gcd(n, g(n-1)), for n > 4.
The first few values are:
<table>
<thead>
<tr>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
<th>&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td>n&nbsp;&nbsp;&nbsp;</td>
<td>4&nbsp;</td>
<td>5&nbsp;</td>
<td>6&nbsp;</td>
<td>7&nbsp;</td>
<td>8&nbsp;</td>
<td>9&nbsp;</td>
<td>10</td>
<td>11</td>
<td>12</td>
<td>13</td>
<td>14</td>
<td>15</td>
<td>16</td>
<td>17</td>
<td>18</td>
<td>19</td>
<td>20</td>
<td>\dots</td>
</tr>
<tr>
<td>g(n)</td>
<td>13</td>
<td>14</td>
<td>16</td>
<td>17</td>
<td>18</td>
<td>27</td>
<td>28</td>
<td>29</td>
<td>30</td>
<td>31</td>
<td>32</td>
<td>33</td>
<td>34</td>
<td>51</td>
<td>54</td>
<td>55</td>
<td>60</td>
<td>\dots</td>
</tr>
</tbody></table>
You are given that g(1&nbsp;000) = 2524 and g(1&nbsp;000&nbsp;000) = 2624152.
Find g(10^15).


## 解决方案


## 代码


