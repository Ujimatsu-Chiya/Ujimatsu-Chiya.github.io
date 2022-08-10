---
title: Project Euler 724
date: 2022-04-22 21:44:30
category:
  - Project Euler
tags:
  - 概率
mathjax: true
---

<escape><!-- more --></escape>

# Project Euler 724

## 题目

### Drone Delivery

A depot uses $n$ drones to disperse packages containing essential supplies along a long straight road.Initially all drones are stationary, loaded with a supply package.

Every second, the depot selects a drone at random and sends it this instruction:

- If you are stationary, start moving at one centimetre per second along the road.
- If you are moving, increase your speed by one centimetre per second along the road without changing direction.

The road is wide enough that drones can overtake one another without risk of collision.

Eventually, there will only be one drone left at the depot waiting to receive its first instruction. As soon as that drone has flown one centimetre along the road, all drones drop their packages and return to the depot.

Let $E(n)$ be the expected distance in centimetres from the depot that the supply packages land. For example, $E(2) = \frac{7}{2}$, $E(5) = \frac{12019}{720}$, and $E(100) \approx 1427.193470$.

Find $E(10^8)$. Give your answer rounded to the nearest integer.

## 赠券收集问题(Coupon collector's problem)

[赠券收集问题](https://en.wikipedia.org/wiki/Coupon_collector%27s_problem): 有买东西的时候会有$n$种不同的卡片赠送，每次等概率地赠送一张，求集齐这些卡片需要购买的产品的数量的期望值。

令$T=\sum_{i=1}^nt_i$，其中$t_i$表示维持在购买了$i-1$张卡片后购买第$i$张的时间。

可以知道，在已经收集到了第$i-1$向赠券的情况下，能够收集第$i$张的概率为$p_i=\dfrac{n-i+1}{n}$，故$t_i$服从参数为$p_i$的几何分布，即$t_i\sim GE(p_i)$.

故$E[t_i]=\dfrac{1}{p_i},D[t_i]=\dfrac{1-p_i}{p_i^2},E[T]=\sum_{i=1}^nE[t_i]$.

另外，可以发现$t_i$之间都是独立的，因为抽到的新赠券的时刻和之前已经抽到的没有什么关系，故$D[T]=\sum_{i=1}^nD[t_i]$.

另外可以计算出$E[T^2]=E^2[T]+D[T]$.

## 解决方案

根据题意，可以得出一个信息：在第$i$秒时下达的指令，到了第$n$秒，这个指令的贡献位$n-i+1$的距离。

为求出平均距离的期望，先求出距离总和的期望。根据上面的结论，如果第$T$秒结束，那么这一段时间产生的距离总和为$\dfrac{T(T+1)}{2}$.

因此距离的总和期望为$E\left[\dfrac{T(T+1)}{2}\right]=\dfrac{1}{2}(E[T]+E[T^2])$.

可以发现，变量$T$是赠券收集问题中的变量。

直接代入问题中的计算结果，可得答案为$e=\dfrac{E[T]+E[T^2]}{2n}$.

## 代码

```C++
# include <bits/stdc++.h>
using namespace std;
/*
https://en.wikipedia.org/wiki/Coupon_collector%27s_problem#Solution
E[tx]表示持有x张票时持续的时间的期望。
tx~E(n/(n-x+1))
E[C]=E[t1]+E[t2]+...+E[tn]=n*H(n)
D[C]=D[t1]+D[t2]+...+D[tn]=n^2(1+1/4+...+1/n^2)。
E[C^2]=E[C]^2+D[C]。
从整体上看，每次都会有一个无人机被添加速度，因此第i秒的操作在前n秒就贡献了n-i+1的距离。
因此答案为E[C(C+1)/2]。
平均下来就是一台无人机可以飞E[C(C+1)/2]/n。
*/
const int N=1e8;
int main(){
    double ec=0,dc=0;
    for(int i=1;i<=N;i++){
        double p=1.0*(N-i+1)/N;
        ec+=1.0/p;
        dc+=(1.0-p)/p/p;
    }
    double ec2=ec*ec+dc;
    double ans=0.5*(ec+ec2)/N;
    printf("%.f\n",ans);
}
```
