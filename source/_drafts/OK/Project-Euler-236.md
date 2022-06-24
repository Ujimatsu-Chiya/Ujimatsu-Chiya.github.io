---
title: Project Euler 236
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    

# Project Euler 236
## 题目
### Luxury Hampers

Suppliers ‘A’ and ‘B’ provided the following numbers of products for the luxury hamper market:

|Product|‘A’|‘B’|
|-|-|-|
|Beluga Caviar|$5248$|$640$|
|Christmas Cake|$1312$|$1888$|
|Gammon Joint|$2624$|$3776$|
|Vintage Port|$5760$|$3776$|
|Champagne Truffles|$3936$|$5664$|

Although the suppliers try very hard to ship their goods in perfect condition, there is inevitably some spoilage - *i.e.* products gone bad.
The suppliers compare their performance using two types of statistic:

- The five *per-product spoilage rates* for each supplier are equal to the number of products gone bad divided by the number of products supplied, for each of the five products in turn.

- The *overall spoilage rate* for each supplier is equal to the total number of products gone bad divided by the total number of products provided by that supplier.

To their surprise, the suppliers found that each of the five per-product spoilage rates was worse (higher) for ‘B’ than for ‘A’ by the same factor (ratio of spoilage rates), $m>1$; and yet, paradoxically, the overall spoilage rate was worse for ‘A’ than for ‘B’, also by a factor of $m$.

There are thirty-five $m>1$ for which this surprising result could have occurred, the smallest of which is $1476/1475$.

What’s the largest possible value of $m$?

Give your answer as a fraction reduced to its lowest terms, in the form $u/v$.


## 解决方案

假设$m=\dfrac{u}{v}$，$\gcd(u,v)=1$，$a_1,a_2,\dots,a_5$分别是$A$店铺对应$5$个商品的损耗量，$b_1,b_2,\dots,b_5$同理。

那么可以写出以下几个等式：

$$\dfrac{b_1}{a_1}=\dfrac{5u}{41v},\dfrac{b_2}{a_2}=\dfrac{b_3}{a_3}=\dfrac{b_5}{a_5}=\dfrac{59u}{41v},\dfrac{b_4}{a_4}=\dfrac{59u}{90v}$$

那么，根据最后一个条件：A点的损耗总数为B的$m$倍，那么可以写出：

$$\dfrac{\sum_{i=1}^5a_i}{\sum_{i=1}^5b_i}=\dfrac{295u}{246v}$$

## 代码


