---
title: Project Euler 610
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 610
## 题目
### Roman Numerals II

A random generator produces a sequence of symbols drawn from the set {<span style="font-family:'courier new', monospace;">I</span>, <span style="font-family:'courier new', monospace;">V</span>, <span style="font-family:'courier new', monospace;">X</span>, <span style="font-family:'courier new', monospace;">L</span>, <span style="font-family:'courier new', monospace;">C</span>, <span style="font-family:'courier new', monospace;">D</span>, <span style="font-family:'courier new', monospace;">M</span>, <span style="font-family:'courier new', monospace;">#</span>}. Each item in the sequence is determined by selecting one of these symbols at random, independently of the other items in the sequence. At each step, the seven letters are equally likely to be selected, with probability 14% each, but the <span style="font-family:'courier new', monospace;">#</span> symbol only has a 2% chance of selection.

We write down the sequence of letters from left to right as they are generated, and we stop at the first occurrence of the <span style="font-family:'courier new', monospace;">#</span> symbol (without writing it). However, we stipulate that what we have written down must always (when non-empty) be a valid Roman numeral representation in minimal form. If appending the next letter would contravene this then we simply skip it and try again with the next symbol generated.

Please take careful note of <a href="about=roman_numerals">About\dots Roman Numerals</a> for the definitive rules for this problem on what constitutes a "valid Roman numeral representation" and "minimal form". For example, the (only) sequence that represents 49 is <span style="font-family:'courier new', monospace;">XLIX</span>. The subtractive combination <span style="font-family:'courier new', monospace;">IL</span> is invalid because of rule (ii), while <span style="font-family:'courier new', monospace;">XXXXIX</span> is valid but not minimal. The rules do not place any restriction on the number of occurrences of <span style="font-family:'courier new', monospace;">M</span>, so all positive integers have a valid representation. These are the same rules as were used in <a href="problem=89">Problem 89</a>, and members are invited to solve that problem first.

Find the expected value of the number represented by what we have written down when we stop. (If nothing is written down then count that as zero.) Give your answer rounded to 8 places after the decimal point.


# Project Euler 610
## 题目
### Roman Numerals II

A random generator produces a sequence of symbols drawn from the set {<span style="font-family:'courier new', monospace;">I</span>, <span style="font-family:'courier new', monospace;">V</span>, <span style="font-family:'courier new', monospace;">X</span>, <span style="font-family:'courier new', monospace;">L</span>, <span style="font-family:'courier new', monospace;">C</span>, <span style="font-family:'courier new', monospace;">D</span>, <span style="font-family:'courier new', monospace;">M</span>, <span style="font-family:'courier new', monospace;">#</span>}. Each item in the sequence is determined by selecting one of these symbols at random, independently of the other items in the sequence. At each step, the seven letters are equally likely to be selected, with probability 14% each, but the <span style="font-family:'courier new', monospace;">#</span> symbol only has a 2% chance of selection.
We write down the sequence of letters from left to right as they are generated, and we stop at the first occurrence of the <span style="font-family:'courier new', monospace;">#</span> symbol (without writing it). However, we stipulate that what we have written down must always (when non-empty) be a valid Roman numeral representation in minimal form. If appending the next letter would contravene this then we simply skip it and try again with the next symbol generated.
Please take careful note of <a href="https://projecteuler.net/about=roman_numerals" target="_blank" rel="noopener">About\dots Roman Numerals</a> for the definitive rules for this problem on what constitutes a “valid Roman numeral representation” and “minimal form”. For example, the (only) sequence that represents 49 is <span style="font-family:'courier new', monospace;">XLIX</span>. The subtractive combination <span style="font-family:'courier new', monospace;">IL</span> is invalid because of rule (ii), while <span style="font-family:'courier new', monospace;">XXXXIX</span> is valid but not minimal. The rules do not place any restriction on the number of occurrences of <span style="font-family:'courier new', monospace;">M</span>, so all integers have a valid representation. These are the same rules as were used in <a href="https://projecteuler.net/problem=89" target="_blank" rel="noopener">Problem 89</a>, and members are invited to solve that problem first.
Find the expected value of the number represented by what we have written down when we stop. (If nothing is written down then count that as zero.) Give your answer rounded to 8 places after the decimal point.


## 解决方案


## 代码


