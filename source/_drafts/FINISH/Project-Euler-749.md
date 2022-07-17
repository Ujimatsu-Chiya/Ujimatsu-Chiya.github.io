---
title: Project Euler 749
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 749
## 题目
### Near Power Sums



A positive integer, $n$, is a *near power sum* if there exists a positive integer, $k$, such that the sum of the $k\text{th}$ powers of the digits in its decimal representation is equal to either $n+1$ or $n-1$. For example $35$ is a near power sum number because $3^2+5^2 = 34$.


Define $S(d)$ to be the sum of all near power sum numbers of $d$ digits or less. 

Then $S(2) = 110$ and $S(6) = 2562701$.


Find $S(16)$.




## 解决方案

令$M=16$，那么不难发现，幂$k$最大只能有$\lfloor M\log_{2}10\rfloor$。

因此先枚举$k$值，然后从大到小枚举$0\sim9$中每个数位可能的出现次数，并在最后计算数位幂和$s$。接下来分别判断$s+1$和$s-1$能不能由这些数位组成，如果成功，那么$s+1$与$s-1$都将是一个候选答案。

还有另外一个优化：当$k$为奇数时，不可能有解。原因如下：

假设当前的一个数为$d=d_{m-1}d_{m-2}\dots d_1d_0$，那么$d=\sum_{i=0}^{m-1}d_i10^i$，其数位幂之和为$\sum_{i=0}^{m-1}d_i^k$。那么可以写成$\sum_{i=0}^{m-1}d_i10^i=\sum_{i=0}^{m-1}d_i^k\pm1.$

那么$\sum_{i=0}^{m-1}(d_i^k-d_i 10^i)\%3\neq0$.

$\sum_{i=0}^{m-1}(d_i^k-d_i 10^i)\%3=\sum_{i=0}^{m-1}(d_i^k-d_i)\%3=\sum_{i=0}^{m-1}(d_i^{k\%2}-d_i)\%3$.

因此，当$k$为奇数时，求和式的值永远为$0$，不满足题目要求。因此搜索时，可以将$k$为奇数跳过。

## 代码


```C++
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=16;
const ll M=pow(10,N);
const int O=log2(10)*N+3;
ll pw[12][O];
int c0[10],c1[10];
int n;
vector<ll>a;
bool ok(ll x){
    memcpy(c1,c0,sizeof(c1));
    for(int i=0;i<N;i++,x/=10)
        if(--c1[x%10]<0) return 0;
    return x==0;
}
void dfs(int k,int n,int p,ll s){
    if(p==0){
        c0[0]=n;
        if(ok(s-1)) a.push_back(s-1);
        if(ok(s+1)) a.push_back(s+1);
        return;
    }
    for(int i=0;i<=n;i++){
        if(pw[p][k]==-1) break;
        c0[p]=i;
        dfs(k,n-i,p-1,s+pw[p][k]*i);
    }
}

int main(){
    memset(pw,-1,sizeof(pw));
    pw[0][0]=1;
    for(int j=1;j<N+N;j++)
        pw[0][j]=0;
    for(int i=0;i<10;i++){
        pw[i][0]=1;
        for(int j=1;j<O;j++){
            pw[i][j]=pw[i][j-1]*i;
            if(i>0&&pw[i][j]>M/i) break;
        }
    }
    for(int k=2;pw[2][k]!=-1;k+=2)
        dfs(k,N,9,0);
    ll ans=0;
    for(ll x:a)
        ans+=x;
    printf("%lld\n",ans);
}

```