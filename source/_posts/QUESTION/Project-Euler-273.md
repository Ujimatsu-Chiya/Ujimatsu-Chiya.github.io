---
title: Project Euler 273
tags:
  - Project Euler
mathjax: true
date: 2022-07-06 13:08:39
---

<escape><!-- more --></escape>

# Project Euler 273

## 题目

### Sum of Squares

Consider equations of the form: $a^2 + b^2 = N$, $0 \le a \le b$, $a, b$ and $N$ integer.

For $N=65$ there are two solutions:$a=1, b=8$ and $a=4, b=7$.

We call $S(N)$ the sum of the values of $a$ of all solutions of $a^2 + b^2 = N$, $0 \le a \le b$, $a, b$ and $N$ integer.

Thus $S(65) = 1 + 4 = 5$.

Find $\sum S(N)$, for all squarefree $N$ only divisible by primes of the form $4k+1$ with $4k+1 < 150$.

## 婆罗摩笈多——斐波那契恒等式

[婆罗摩笈多——斐波那契恒等式](https://en.wikipedia.org/wiki/Brahmagupta%E2%80%93Fibonacci_identity)说明，如果两个整数分别能表示成两个平方数之和，那么这两个整数的积也能表示成两个平方数之和：

$$(a^2+b^2)(c^2+d^2)=(ac-bd)^2+(ad+bc)^2=(ac+bd)^2+(ad-bc)^2$$

## 解决方案

[页面1](https://en.wikipedia.org/wiki/Fermat%27s_theorem_on_sums_of_two_squares)，[页面2](https://en.wikipedia.org/wiki/Pythagorean_prime#Representation_as_a_sum_of_two_squares)说明了一个奇质数当且仅当它模$4$余$1$，才能表示成两个不同平方数之和，并且表示方式是**唯一**的。

我们先求出$M=150$以内的所有模$4$余$1$的唯一平方数之和的表示$p_i=a_i^2+b_i^2$，然后根据婆罗摩笈多——斐波那契恒等式，将每一对表示方式进行不同的组合即可。

## 代码

```C++
# include <bits/stdc++.h>
# include "tools.h"
using namespace std;
typedef long long ll;
const int N=150;
vector<int>pr,u,v;
ll dfs(int f,ll a,ll b){
    if(f==u.size()) return min(abs(a),abs(b));
    return dfs(f+1,a,b)+dfs(f+1,a*u[f]-b*v[f],a*v[f]+b*u[f])+dfs(f+1,a*u[f]+b*v[f],a*v[f]-b*u[f]);
}
int main() {
    for(int p=1;p<N;p+=4)
        if(is_prime(p)){
            pr.push_back(p);
            for(int a=1;a*a<=p;a++){
                int b=int_square(p-a*a);
                if(a*a+b*b==p){
                    u.push_back(a);
                    v.push_back(b);
                    break;
                }
            }
        }
    ll ans=0;
    for(int i=0;i<u.size();i++)
        ans+=dfs(i+1,u[i],v[i]);
    printf("%lld\n", ans);
}

```
