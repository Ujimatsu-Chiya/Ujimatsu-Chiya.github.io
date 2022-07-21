---
title: Project Euler 318
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 318
## 题目
### 2011 nines



Consider the real number $\sqrt 2 + \sqrt 3$.
When we calculate the even powers of $\sqrt 2 + \sqrt 3$
we get:

$\begin{aligned}
&(\sqrt 2 + \sqrt 3)^2 = 9.898979485566356 \dots \\
&(\sqrt 2 + \sqrt 3)^4 = 97.98979485566356 \dots \\
&(\sqrt 2 + \sqrt 3)^6 = 969.998969071069263 \dots\\
&(\sqrt 2 + \sqrt 3)^8 = 9601.99989585502907 \dots \\
&(\sqrt 2 + \sqrt 3)^{10} = 95049.999989479221 \dots \\
&(\sqrt 2 + \sqrt 3)^{12} = 940897.9999989371855 \dots \\
&(\sqrt 2 + \sqrt 3)^{14} = 9313929.99999989263 \dots \\
&(\sqrt 2 + \sqrt 3)^{16} = 92198401.99999998915 \dots \\
\end{aligned}$

It looks as if the number of consecutive nines at the beginning of the fractional part of these powers is non-decreasing.

In fact it can be proven that the fractional part of $(\sqrt 2 + \sqrt 3)^{2 n}$ approaches $1$ for large $n$.


Consider all real numbers of the form $\sqrt p + \sqrt q$ with $p$ and $q$ positive integers and $p < q$, such that the fractional part 
of $(\sqrt p + \sqrt q)^{ 2 n}$ approaches $1$ for large $n$.


Let $C(p,q,n)$ be the number of consecutive nines at the beginning of the fractional part of $(\sqrt p + \sqrt q)^{ 2 n}$.


Let $N(p,q)$ be the minimal value of $n$ such that $C(p,q,n) \ge 2011$.


Find $\displaystyle \sum N(p,q) \,\, \text{ for } p+q \le 2011$.



## 解决方案


## 代码


```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=2011,M=2011;
double sq[N+4];
int main(){
    for(int i=1;i<=N;i++)
        sq[i]=sqrt(i);
    ll ans=0;
    for(int p=1;p<=N;p++)
        for(int q=p+1;p+q<=N&&sq[q]-sq[p]<1;q++){
            double g=-log10(sq[q]-sq[p])*2;
            ans+=ceil(1.0*M/g);
        }
    printf("%lld\n",ans);
}

```