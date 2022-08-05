---
title: Project Euler 720
tags:
  - Project Euler
  - 树状数组
mathjax: true
date: 2022-08-05 21:41:32
---

<escape><!-- more --></escape>

# Project Euler 720

## 题目

### Unpredictable Permutations

Consider all permutations of $\{1, 2, \ldots N\}$, listed in lexicographic order.

For example, for $N=4$, the list starts as follows:

$$\begin{aligned}
(1, 2, 3, 4) \\
(1, 2, 4, 3) \\
(1, 3, 2, 4) \\
(1, 3, 4, 2) \\
(1, 4, 2, 3) \\
(1, 4, 3, 2) \\
(2, 1, 3, 4) \\
\vdots
\end{aligned}$$

Let us call a permutation $P$ *unpredictable* if there is no choice of three indices $i \lt j \lt k$ such that $P(i)$, $P(j)$ and $P(k)$ constitute an arithmetic progression.<br /> For example, $P=(3, 4, 2, 1)$ is *not* unpredictable because $P(1), P(3), P(4)$ is an arithmetic progression.

Let $S(N)$ be the position within the list of the first unpredictable permutation.

For example, given $N = 4$, the first unpredictable permutation is $(1, 3, 2, 4)$ so $S(4) = 3$.

You are also given that $S(8) = 2295$ and $S(32) \equiv 641839205 \pmod{1\,000\,000\,007}$.

Find $S(2^{25})$. Give your answer modulo $1\,000\,000\,007$.

## 解决方案

令$N=25$。本题主要依靠打表找规律的方法解决。

使用以下程序分别暴力打印出题目所需要的$2,4,8,16$阶排列：

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
int a[18],n;
bool b[18];
bool dfs(int f){
    if(f==n+1){
        printf("%2d:",n);
        for(int i=1;i<=n;i++)
            printf("%2d%c",a[i]," \n"[i==n]);
        return 1;
    }
    else{
        for(int k=1;k<=n;k++){
            if(b[k]) continue;
            bool ok=1;
            for(int j=1;j<f&&ok;j++)
                for(int i=1;i<j&&ok;i++)
                    if((a[j]<<1)==a[i]+k) ok=0;
            if(ok){
                b[k]=1;
                a[f]=k;
                if(dfs(f+1)) return 1;
                b[k]=0;
            }
        }
    }
    return 0;
}
int main(){
    for(n=2;n<=16;n<<=1){
        memset(b,0,sizeof(b));
        dfs(1);
    }
}

```

结果如下：

```
 2: 1  2
 4: 1  3  2  4
 8: 1  5  3  2  7  6  4  8
16: 1  9  5  3 13 11  7  2 15 10  6  4 14 12  8 16
```

从第$4$个排列起，可以发现，第$2n$个排列$P_{2n}$可以由第$n$个排列$P_n$产生而来：

- 先将$P_n$中的所有数全部乘$2$，拼在$P_{2n}$的右半部分。
- 再将$P_n$中的所有数全部乘$2$再减去$1$，拼在$P_{2n}$的左半部分。
- 将中间的两个数交换，最终结果就是$P_{2n}$。

这个过程可以在线性的时间复杂度完成。

构造完这个排列后，基于康托展开的思想，使用树状数组直接计算这个排列的编码即可。时间复杂度为$O(N\cdot 2^N)$。

由于这个排列比较特殊，我们可以用一个数组$c$来维护$P_n$排列的信息：$c_n[i]$表示$P_n(i)$中右边有多少个数小于$P_n(i)$。

对于左半部分，由于左半部分恰好是右半部分中每个数减去$1$，因此$c_{2n}[i]=c_n[i]+P_n(i)-1$；右半部分和$P_n$的相对大小没有变化，因此$P_{2n}(i+n)=P_n(i)$。

不过，上面的结论对$i=n,n-1$时不成立，因为它还忽略了上面构造排列的第三个步骤。考虑第三个步骤后，$P_{2n}(n-1)=2$，因此$c_{2n}[n-1]=0$。更小的$2$被换到前面，那么实际上还需要减去$1$，因此$c_{2n}[n]=P_n(n-1)+c_n[n-1]-2$。

那么最终答案为$\sum_{i=0}^{2^N-1} i!\cdot c_{2^N}[2^N-1-i]$，以更快的效率将康托展开系数处理了出来。

## 代码

```C++
#include <bits/stdc++.h>
#define lb(x) ((x)&-(x))
using namespace std;
typedef long long ll;
const int N=25;
const int M=1<<N;
int a[M]={1,3,2,4},m=4;
int fac[M+1],mod=1000000007;
void add(int &x, int y) {
    (x += y) >= mod && (x -= mod);
}
int s[M+1];
void update(int p){
    for(int i=p;i<=M;i+=lb(i))
        ++s[i];
}
int que(int p){
    int ans=0;
    for(int i=p;i;i-=lb(i))
        add(ans,s[i]);
    return ans;
}
int main(){
    fac[0]=1;
    for(int i=1;i<=M;i++)
        fac[i]=1ll*fac[i-1]*i%mod;
    while(m<M){
        for(int i=0;i<m;i++){
            a[m+i]=a[i]*2;
            a[i]=a[i]*2-1;
        }
        swap(a[m],a[m-1]);
        m<<=1;
    }
    int ans=1;
    for(int i=0;i<M;i++){
        add(ans,1ll*(a[i]-que(a[i])-1)*fac[M-i-1]%mod);
        update(a[i]);
    }
    printf("%d\n",ans);
}

```

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=25;
const int M=1<<N;
int a[M]={1,3,2,4},m=4;
int c[M]={0,1,0,0};
int mod=1000000007;
int main(){
    while(m<M){
        for(int i=0;i<m;i++)
            c[i+m]=c[i];
        c[m]=c[m-1]+a[m-1]-2;
        for(int i=0;i<m;i++)
            c[i]+=a[i]-1;
        c[m-1]=0;
        for(int i=0;i<m;i++){
            a[m+i]=a[i]*2;
            a[i]=a[i]*2-1;
        }
        swap(a[m],a[m-1]);
        m<<=1;

    }
    ll ans=1,fac=1;
    for(int i=0;i<M;i++){
        ans=(fac*c[M-1-i]+ans)%mod;
        fac=fac*(i+1)%mod;
    }
    printf("%lld\n",ans);
}

```
