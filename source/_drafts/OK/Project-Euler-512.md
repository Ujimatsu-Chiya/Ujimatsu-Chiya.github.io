---
title: Project Euler 512
tags:
  - Project Euler
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

令$\Phi_k(n)=\sum_{i=1,k|i}^n \varphi(n)$，那么$g(n)=\Phi(n)-\Phi_2(n)$。$\Phi_k(n)$满足：

$$\Phi_k(n)=\Phi(\dfrac{n}{k})+\Phi(\dfrac{n}{k^2})+\Phi(\dfrac{n}{k^3})+\dots$$

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