---
title: Project Euler 655
tags:
  - Project Euler
mathjax: true
date: 2022-08-05 21:40:40
---

<escape><!-- more --></escape>

# Project Euler 655

## 题目

### Divisible Palindromes

The numbers $545$, $5\,995$ and $15\,151$ are the three smallest **palindromes** divisible by $109$. There are nine palindromes less than $100\,000$ which are divisible by $109$.

How many palindromes less than $10^{32}$ are divisible by $10\,000\,019\,$ ?

## 解决方案

令$N=32,P=10000019$。考虑使用动态规划解决本题。

为了减少时间复杂度，本题将考虑有前导$0$的情况。也就是说，如果需要求$N=7$以内的情况，那么一个$3$位的回文数前后将会各自补充两个零，从而形成$7$位的情况。这种方法只有当满足$\gcd(P,10)=1$时才使用。

我们考虑将回文数的对应两个数位“捆绑”在一起，然后将它们的系数放入数组$c$中。也就是说，$c=[10^0+10^{N-1},10^1+10^{N-2},\dots,10^i+10^{N-i-1}]$。如果$N$还是一个奇数，那么还需要再将$10^{\frac{N-1}{2}}$放入$c$中。那么，对于一个数位$d_1,d_2,\dots,d_{m}\in[0,9]$，$\sum_{i=1}^{m} c[i]\cdot d_i$将会组合出一个个$N$位**有前导**$0$回文数。

令数组$c$的长度为$M$，也就是有$M=\lfloor\dfrac{N+1}{2}\rfloor$。令状态$f(i,j)(0\le i\le M,0 \le j< P)$表示当前使用了$c$数组中前$i$个系数，组合出了模$P$为$j$的数的个数。不难写出$f$的状态转移方程为：

$$
f(i,j)=
\left \{\begin{aligned}
  &1 & & \mathrm{if\quad} i=1\wedge j=0 \\
  &0 & & \mathrm{else if\quad} i=1 \\
  &\sum_{d=0}^9\sum_{(k+c[i]\cdot d)\%p=j} f(i-1,k) & & \mathrm{else}
\end{aligned}\right.
$$

那么$f(i,j)$就代表了$i,i-2,i-4,\dots$位无前导$0$且模$P$为$j$的回文数个数。

最终答案为$f(M,0)+f(M-1,0)$。

## 代码

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int P=10000019;
const int N=32;
int pw[N+4];
ll f[2][P];
int con[N+4],m=0;
ll solve(int n){
    m=0;
    for(int i=0;i<n/2;i++)
        con[m++]=pw[i]+pw[n-1-i];
    if(n&1) con[m++]=pw[n/2];
    memset(f[0],0,sizeof(f[0]));
    f[0][0]=1;
    for(int i=0,p=0;i<m;i++,p^=1){
        memset(f[p^1],0,sizeof(f[p^1]));
        for(int j=0;j<P;j++){
            if(f[p][j]==0) continue;
            for(int k=0;k<10;k++)
                f[p^1][(j+con[i]*k)%P]+=f[p][j];
        }
    }
    return f[m&1][0]-1;
}
int main(){
    pw[0]=1;
    for(int i=1;i<=N;i++)
        pw[i]=pw[i-1]*10%P;
    ll ans=solve(N)+solve(N-1);
    printf("%lld\n",ans);
}

```
