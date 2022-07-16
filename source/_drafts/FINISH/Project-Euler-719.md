---
title: Project Euler 719
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 719
## 题目
### Number Splitting



We define an $S$-number to be a natural number, $n$, that is a perfect square and its square root can be obtained by splitting the decimal representation of $n$ into $2$ or more numbers then adding the numbers.


For example, $81$ is an $S$-number because $\sqrt{81} = 8+1$.

$6724$ is an $S$-number: $\sqrt{6724} = 6+72+4$. 

$8281$ is an $S$-number: $\sqrt{8281} = 8+2+81 = 82+8+1$.

$9801$ is an $S$-number: $\sqrt{9801}=98+0+1$.


Further we define $T(N)$ to be the sum of all $S$ numbers $n\le N$. You are given $T(10^4) = 41333$.


Find $T(10^{12})$



## 解决方案

对于$n>1$，永远不会出现$n^2=n$的情况，因此这里不需要判断一个正确的划分方案是否只有一个数（而不是多个数相加）。

另外一个优化之处则是只有当$n\%9<2$时，$n^2$才有可能是一个候选答案，原因：假设$d$是$n$的各位数字之和，那么无论等式右侧的数如何划分，它们的数位和模$9$和$n^2$的数位和模$9$是一样的。根据$S$数的定义，$n$和这些划分后的数位值相加相等，因此$n^2\equiv n(\mod 9).$

其余的部分则使用深度优先搜索对$n$进行判断，在判断的过程中，注意加法的每个项不可能超过$n$.

## 代码


```C++
# include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll N=1e12;
ll m;
int a[25],p=0;
bool dfs(int f,ll s,ll w){
    if(s>m||w>m) return 0;
    if(f==p) return s+w==m;
    if(dfs(f+1,s+w,a[f])||dfs(f+1,s,w*10+a[f])) return 1;
    return 0;
}
int main(){
    ll ans=0;
    for(m=4;m*m<=N;m++){
        if(m%9>1) continue;
        ll t=m*m;
        p=0;
        for(;t;t/=10) a[p++]=t%10;
        reverse(a,a+p);
        if(dfs(0,0,0)) ans+=m*m;
    }
    printf("%lld\n",ans);
}

```