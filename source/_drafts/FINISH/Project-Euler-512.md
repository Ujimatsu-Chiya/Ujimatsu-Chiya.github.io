---
title: Project Euler 512
tags:
  - Project Euler
  - 数论分块
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 512
## 题目
### Sums of totients of powers


Let $\varphi(n)$ be Euler's totient function.

Let $f(n)=(\sum_{i=1}^{n}\varphi(n^i)) \text{ mod } (n+1)$.

Let $g(n)=\sum_{i=1}^{n} f(i)$.

$g(100)=2007$.

Find $g(5 \times 10^8)$.



## 解决方案

根据欧拉函数的性质，不难写出$\varphi(n^i)=\varphi (n)\cdot n^{i-1}$

$f(n)=\sum_{i=1}^n\varphi(n^i)=\varphi(n)\sum_{i=0}^{n-1} n^i$

因此$f(n) = \varphi(n)\cdot \sum_{i=0}^{n-1}(-1)^i\mod (n+1)$。

如果$n$为偶数，那么$f(n) =  0\mod (n+1)$

如果$n$为奇数，那么$f(n)=\varphi(n) \mod (n+1)$

因此，

$$g(n)=\sum_{i=1}^{\lfloor\dfrac{n+1}{2}\rfloor}\varphi(2i-1)$$

可以直接使用筛法计算奇数的欧拉函数值。

为了使用数论分块加速，考虑

$$\Phi(n)=\sum_{i=1}^n\varphi(n)$$

令$\Phi_p(n)=\sum_{i=1,p|i}^n \varphi(n)$，$p$是一个质数。那么$g(n)=\Phi(n)-\Phi_2(n)$。$\Phi_p(n)$满足：

$$\Phi_p(n)=\varphi(p)\cdot(\Phi(\dfrac{n}{p})+\Phi(\dfrac{n}{p^2})+\Phi(\dfrac{n}{p^3})+\dots)$$

说明：如果一个数$p^k\cdot x,p\nmid x,k>1$，那么$\varphi(p^k\cdot x)=(p-1)p^{k-1}x$。因此，在上面的式子中，$\varphi(p^k\cdot x)$的一部分被算进$\varphi(p)\cdot\Phi(\dfrac{n}{p^k})$，另一部分被算进$\varphi(p)\cdot\Phi(\dfrac{n}{p^{k-1}})$。

那么现在的问题就是使用数论分块的方法高效计算$\Phi(n)$的值。

$$\begin{aligned}
\dfrac{n(n+1)}{2}&=|\{(a,b)|1\le a\le b \le n\}|\\
&=\sum_{d=1}^n\{(a,b)|1\le a\le b \le n,\gcd(a,b)=d\}|\\
&=\sum_{d=1}^n\{(a,b)|1\le a\le b \le \lfloor\dfrac{n}{d}\rfloor,\gcd(a,b)=1\}\\
&=\sum_{d=1}^n\Phi(\dfrac{n}{d})
\end{aligned}$$

因此，可以得到关于$\Phi$的递归式：

$$\Phi(n)=\dfrac{n(n+1)}{2}-\sum_{d=2}^n\Phi(\dfrac{n}{d})$$

其中，右边这一部分可以使用数论分块来解决。

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=5e8;
const int M=(N+1)>>1;
int phi[M+2];
int main(){
    for(int i=1;i<=M;i++)
        phi[i]=2*i-1;
    for(int i=2;i<=M;i++){
        int v=2*i-1;
        if(phi[i]==v){
            for(int j=i;j<=M;j+=v)
                phi[j]=phi[j]/v*(v-1);
        }
    }
    ll ans=0;
    for(int i=1;i<=M;i++)
        ans+=phi[i];
    printf("%lld\n",ans);
}
```

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=5e8;
const int M= pow(N,2.0/3);
ll s[M+2];
int v[M+2],pr[M/10+1000],m=0;
unordered_map<ll,ll>mp;
ll sum_phi(ll n){
    if(n<=M) return s[n];
    else if(mp.count(n)) return mp[n];
    ll ans=n*(n+1)/2;
    for(ll l=2,r;l<=n;l=r+1){
        r=n/(n/l);
        ans-=(r-l+1)* sum_phi(n/l);
    }
    return mp[n]=ans;
}
int main(){
    s[1]=1;
    for(int i=2;i<=M;i++) {
        if(v[i]==0){
            v[i]=i;pr[++m]=i;s[i]=i-1;
        }
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>M/i) break;
            v[i*pr[j]]=pr[j];
            s[i*pr[j]]=s[i]*(pr[j]==v[i]?pr[j]:pr[j]-1);
        }
    }
    for(int i=2;i<=M;i++)
        s[i]+=s[i-1];
    ll ans = sum_phi(N);
    for(ll i=2;i<=N;i*=2)
        ans -= sum_phi(N/i);
    printf("%lld\n",ans);
}
```