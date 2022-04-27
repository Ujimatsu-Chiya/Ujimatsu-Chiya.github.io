---
title: Project Euler 196
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 196
## 题目
### Prime triplets

Build a triangle from all positive integers in the following way:

<p style="font-family:'courier new', monospace;font-weight:bold;margin-left:50px;"> 1<br />
 <span style="color:#FF0000;">2</span>  <span style="color:#FF0000;">3</span><br />
 4  <span style="color:#FF0000;">5</span>  6<br />
 <span style="color:#FF0000;">7</span>  8  9 10<br /><span style="color:#FF0000;">11</span> 12 <span style="color:#FF0000;">13</span> 14 15<br />
16 <span style="color:#FF0000;">17</span> 18 <span style="color:#FF0000;">19</span> 20 21<br />
22 <span style="color:#FF0000;">23</span> 24 25 26 27 28<br /><span style="color:#FF0000;">29</span> 30 <span style="color:#FF0000;">31</span> 32 33 34 35 36<br /><span style="color:#FF0000;">37</span> 38 39 40 <span style="color:#FF0000;">41</span> 42 <span style="color:#FF0000;">43</span> 44 45<br />
46 <span style="color:#FF0000;">47</span> 48 49 50 51 52 <span style="color:#FF0000;">53</span> 54 55<br />
56 57 58 <span style="color:#FF0000;">59</span> 60 <span style="color:#FF0000;">61</span> 62 63 64 65 66<br />
. . .

Each positive integer has up to eight neighbours in the triangle.

A set of three primes is called a <i>prime triplet</i> if one of the three primes has the other two as neighbours in the triangle.

For example, in the second row, the prime numbers 2 and 3 are elements of some prime triplet.

If row 8 is considered, it contains two primes which are elements of some prime triplet, i.e. 29 and 31.<br />
If row 9 is considered, it contains only one prime which is an element of some prime triplet: 37.

Define S(<var>n</var>) as the sum of the primes in row <var>n</var> which are elements of any prime triplet.<br />
Then S(8)=60 and S(9)=37.

You are given that S(10000)=950007619.

Find  S(5678027) + S(7208785).



# Project Euler 196
## 题目
### Prime triplets
Build a triangle from all positive integers in the following way:
<table>
<thead>
<tr>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
<th align="right">&nbsp;</th>
</tr>
</thead>
<tbody><tr>
<td align="right">1</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right"><span style="color:red;">2</span></td>
<td align="right"><span style="color:red;">3</span></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right">4</td>
<td align="right"><span style="color:red;">5</span></td>
<td align="right">6</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right"><span style="color:red;">7</span></td>
<td align="right">8</td>
<td align="right">9</td>
<td align="right">10</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right"><span style="color:red;">11</span></td>
<td align="right">12</td>
<td align="right"><span style="color:red;">13</span></td>
<td align="right">14</td>
<td align="right">15</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right">16</td>
<td align="right"><span style="color:red;">17</span></td>
<td align="right">18</td>
<td align="right"><span style="color:red;">19</span></td>
<td align="right">20</td>
<td align="right">21</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right">22</td>
<td align="right"><span style="color:red;">23</span></td>
<td align="right">24</td>
<td align="right">25</td>
<td align="right">26</td>
<td align="right">27</td>
<td align="right">28</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right"><span style="color:red;">29</span></td>
<td align="right">30</td>
<td align="right"><span style="color:red;">31</span></td>
<td align="right">32</td>
<td align="right">33</td>
<td align="right">34</td>
<td align="right">35</td>
<td align="right">36</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right"><span style="color:red;">37</span></td>
<td align="right">38</td>
<td align="right">39</td>
<td align="right">40</td>
<td align="right"><span style="color:red;">41</span></td>
<td align="right">42</td>
<td align="right"><span style="color:red;">43</span></td>
<td align="right">44</td>
<td align="right">45</td>
<td align="right"></td>
<td align="right"></td>
</tr>
<tr>
<td align="right">46</td>
<td align="right"><span style="color:red;">47</span></td>
<td align="right">48</td>
<td align="right">49</td>
<td align="right">50</td>
<td align="right">51</td>
<td align="right">52</td>
<td align="right"><span style="color:red;">53</span></td>
<td align="right">54</td>
<td align="right">55</td>
<td align="right"></td>
</tr>
<tr>
<td align="right">56</td>
<td align="right">57</td>
<td align="right">58</td>
<td align="right"><span style="color:red;">59</span></td>
<td align="right">60</td>
<td align="right"><span style="color:red;">61</span></td>
<td align="right">62</td>
<td align="right">63</td>
<td align="right">64</td>
<td align="right">65</td>
<td align="right">66</td>
</tr>
<tr>
<td align="right">..</td>
<td align="right">..</td>
<td align="right">..</td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
<td align="right"></td>
</tr>
</tbody></table>
Each positive integer has up to eight neighbours in the triangle.
A set of three primes is called a <em>prime triplet</em> if one of the three primes has the other two as neighbours in the triangle.
For example, in the second row, the prime numbers 2 and 3 are elements of some prime triplet.
If row 8 is considered, it contains two primes which are elements of some prime triplet, i.e. 29 and 31.<br>If row 9 is considered, it contains only one prime which is an element of some prime triplet: 37.
Define S(n) as the sum of the primes in row n which are elements of any prime triplet.<br>Then S(8)=60 and S(9)=37.
You are given that S(10000)=950007619.
Find &nbsp;S(5678027) + S(7208785).


## 解决方案


## 代码


