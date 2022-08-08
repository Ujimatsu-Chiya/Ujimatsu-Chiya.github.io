---
title: Project Euler 527
category:
  - Project Euler
tags:
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 527
## 题目
### Randomized Binary Search


A secret integer <var>t</var> is selected at random within the range 1 \le <var>t</var> \le <var>n</var>. 

The goal is to guess the value of <var>t</var> by making repeated guesses, via integer <var>g</var>. After a guess is made, there are three possible outcomes, in which it will be revealed that either <var>g</var> < <var>t</var>, <var>g</var> = <var>t</var>, or <var>g</var> > <var>t</var>. Then the process can repeat as necessary.

Normally, the number of guesses required on average can be minimized with a binary search: Given a lower bound <var>L</var> and upper bound <var>H</var> (initialized to <var>L</var> = 1 and <var>H</var> = <var>n</var>), let <var>g</var> = ⌊(<var>L</var>+<var>H</var>)/2⌋ where ⌊⋅⌋ is the integer floor function. If <var>g</var> = <var>t</var>, the process ends. Otherwise, if <var>g</var> < <var>t</var>, set <var>L</var> = <var>g</var>+1, but if <var>g</var> > <var>t</var> instead, set <var>H</var> = <var>g</var>−1. After setting the new bounds, the search process repeats, and ultimately ends once <var>t</var> is found. Even if <var>t</var> can be deduced without searching, assume that a search will be required anyway to confirm the value.

Your friend Bob believes that the standard binary search is not that much better than his randomized variant: Instead of setting <var>g</var> = ⌊(<var>L</var>+<var>H</var>)/2⌋, simply let <var>g</var> be a random integer between <var>L</var> and <var>H</var>, inclusive. The rest of the algorithm is the same as the standard binary search. This new search routine will be referred to as a <i>random binary search</i>.

Given that 1 \le <var>t</var> \le <var>n</var> for random <var>t</var>, let B(<var>n</var>) be the expected number of guesses needed to find <var>t</var> using the standard binary search, and let R(<var>n</var>) be the expected number of guesses needed to find <var>t</var> using the random binary search. For example, B(6) = 2.33333333 and R(6) = 2.71666667 when rounded to 8 decimal places.

Find R(10^10) − B(10^10) rounded to 8 decimal places.


# Project Euler 527
## 题目
### Randomized Binary Search

A secret integer t is selected at random within the range 1 \le t \le n. 
The goal is to guess the value of t by making repeated guesses, via integer g. After a guess is made, there are three possible outcomes, in which it will be revealed that either g < t, g = t, or g > t. Then the process can repeat as necessary.
Normally, the number of guesses required on average can be minimized with a binary search: Given a lower bound L and upper bound H (initialized to L = 1 and H = n), let g = ⌊(L+H)/2⌋ where ⌊⋅⌋ is the integer floor function. If g = t, the process ends. Otherwise, if g < t, set L = g+1, but if g > t instead, set H = g−1. After setting the new bounds, the search process repeats, and ultimately ends once t is found. Even if t can be deduced without searching, assume that a search will be required anyway to confirm the value.
Your friend Bob believes that the standard binary search is not that much better than his randomized variant: Instead of setting g = ⌊(L+H)/2⌋, simply let g be a random integer between L and H, inclusive. The rest of the algorithm is the same as the standard binary search. This new search routine will be referred to as a <em>random binary search</em>.
Given that 1 \le t \le n for random t, let B(n) be the expected number of guesses needed to find t using the standard binary search, and let R(n) be the expected number of guesses needed to find t using the random binary search. For example, B(6) = 2.33333333 and R(6) = 2.71666667 when rounded to 8 decimal places.
Find R(10^10) − B(10^10) rounded to 8 decimal places.


## 解决方案


## 代码


