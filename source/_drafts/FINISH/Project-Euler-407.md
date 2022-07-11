---
title: Project Euler 407
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    


# Project Euler 407
## 题目
### Idempotents

If we calculate $a^2 \mod 6$ for $0 \le a \le 5$ we get: $0,1,4,3,4,1$.

The largest value of a such that $a^2 ≡ a \mod 6$ is $4$.

Let’s call $M(n)$ the largest value of $a < n$ such that $a^2 \equiv a (\mod n)$. So $M(6) = 4$.

Find $\sum M(n)$ for $1 \le n \le 10^7$.


## 解决方案

可以得到，原方程可以化简为：

$$a(a-1)\equiv 0(\mod n)\qquad(1)$$

由于$\gcd(a,a-1)=1$，假设$n$的分解质因数为$n=\prod_{i=1}^{k} p_i^{e_i}$，那么对于任意一个$p_i^{e_i}$，要么$p_i^{e_i}|a$，要么$p_i^{e_i}|(a-1)$。

那么枚举$\{1,2,\dots,k\}$的所有子集$\{i_1,i_2,\dots,i_m\}$，令$m_1=\prod_{j=1}^mp_{i_j}^{e_{i_j}},m_2=\dfrac{n}{m_1}$，那么方程$(1)$的一个解$a$就可以通过这个方程组构造出来：

$$\left \{\begin{aligned}
  & a\equiv 0(\mod m_1)\\
  & a\equiv 1(\mod m_2)\\
\end{aligned}\right.$$

那么$a$可以很简单地表示成$a=m_1\cdot \text{inv}(m_1,m_2)$，其中$\text{inv}(a,m)$表示$a\%m$在群$\mathbb{Z}_m^{\star}$上的逆元。

此外，为了能够尽快分解质因数，我们首先将$N=10^7$以内的所有数的最大质因数$g(n)$求出，在正式分解$N$的时候能够根据$g(n)$有效加速。

最终，直接枚举每个$n$并求解即可。

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=1e7;
int mxp[N+4],r[14],m;
int inv(int a,int m)
{
	int b=m,x=1,y=0,t;
	while(b){
		int q=a/b;
		t=a-q*b;a=b;b=t;
		t=x-q*y;x=y;y=t;
	}
	return x<0?x+m:x;
}
int main(){
    for(int p=2;p<=N;p++)
        if(!mxp[p])
            for(int i=p;i<=N;i+=p) mxp[i]=p;
    ll ans=0;
    for(int n=1;n<=N;n++){
        m=0;
        for(int x=n;x!=1;){
            int w=1,p=mxp[x];
            for(;x%p==0;x/=p,w*=p);
            r[m++]=w;
        }
        ll mx=0;
        for(int s=0;s<(1<<m);s++){
            ll m1=1,m2=1;
            for(int i=0;i<m;i++)
                s>>i&1?m1*=r[i]:m2*=r[i];
            mx=max(mx,m1*inv(m1,m2));
        }
        ans+=mx;
    }
    printf("%lld\n",ans);
}

```