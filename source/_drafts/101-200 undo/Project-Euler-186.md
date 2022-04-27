---
title: Project Euler 186
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 186
## 题目
### Connectedness of a network

Here are the records from a busy telephone system with one million users:
<div class="center">
<table class="grid" style="margin:0 auto;"><tr><th>RecNr</th><th width="60" align="center">Caller</th><th width="60" align="center">Called</th></tr><tr><td align="center">1</td><td align="center">200007</td><td align="center">100053</td></tr><tr><td align="center">2</td><td align="center">600183</td><td align="center">500439</td></tr><tr><td align="center">3</td><td align="center">600863</td><td align="center">701497</td></tr><tr><td align="center">\dots</td><td align="center">\dots</td><td align="center">\dots</td></tr></table>

# Project Euler 186
## 题目
### Connectedness of a network
Here are the records from a busy telephone system with one million users:
<table>
<thead>
<tr>
<th align="center">Rec Nr</th>
<th align="center">Caller</th>
<th align="center">Called</th>
</tr>
</thead>
<tbody><tr>
<td align="center">1</td>
<td align="center">200007</td>
<td align="center">100053</td>
</tr>
<tr>
<td align="center">2</td>
<td align="center">600183</td>
<td align="center">500439</td>
</tr>
<tr>
<td align="center">3</td>
<td align="center">600863</td>
<td align="center">701497</td>
</tr>
<tr>
<td align="center">\dots</td>
<td align="center">\dots</td>
<td align="center">\dots</td>
</tr>
</tbody></table>
The telephone number of the caller and the called number in record n are Caller(n) = S_2n-1 and Called(n) = S_2n where S_1,2,3,\dots come from the “Lagged Fibonacci Generator”:
For 1 ≤ k ≤ 55, S_k = [100003 - 200003k + 300007k^3] (modulo 1000000)<br>For 56 ≤ k, S_k = [S_k-24 + S_k-55] (modulo 1000000)
If Caller(n) = Called(n) then the user is assumed to have misdialled and the call fails; otherwise the call is successful.
From the start of the records, we say that any pair of users X and Y are friends if X calls Y or vice-versa. Similarly, X is a friend of a friend of Z if X is a friend of Y and Y is a friend of Z; and so on for longer chains.
The Prime Minister’s phone number is 524287. After how many successful calls, not counting misdials, will 99% of the users (including the PM) be a friend, or a friend of a friend etc., of the Prime Minister?


## 解决方案


## 代码


