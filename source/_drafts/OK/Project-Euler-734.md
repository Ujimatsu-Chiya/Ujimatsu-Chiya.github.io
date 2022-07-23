---
title: Project Euler 734
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 734
## 题目
### A bit of prime



The *logical-OR* of two bits is $0$ if both bits are $0$, otherwise it is $1$.

The *bitwise-OR* of two positive integers performs a <i>logical OR</i> operation on each pair of corresponding bits in the binary expansion of its inputs.


For example, the bitwise-OR of $10$ and $6$ is $14$ because $10 = 1010_2$, $6 = 0110_2$ and $14 = 1110_2$.


Let $T(n, k)$ be the number of $k$-tuples $(x_1, x_2,\cdots,x_k)$ such that

 - every $x_i$ is a prime $\leq n$
 - the bitwise-OR of the tuple is a prime $\leq n$

For example, $T(5, 2)=5$. The five $2$-tuples are $(2, 2), (2, 3), (3, 2), (3, 3)$ and $(5, 5)$.

You are given $T(100, 3) = 3355$ and $T(1000, 10) \equiv 2071632 \pmod{1\,000\,000\,007}$


Find $T(10^6,999983)$. Give your answer modulo $1\,000\,000\,007$


## 解决方案


## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N=1000000;
const int M=999983;
int mod = 1000000007;

void add(int &x, int y) {
    (x += y) >= mod && (x -= mod);
}
void sub(int &x, int y) {
    (x -= y) < 0 && (x += mod);
}
struct FWT {
    int extend(int n) {
        int N = 1;
        for (; N < n; N <<= 1);
        return N;
    }
    void FWTor(std::vector<int> &a, bool rev) {
        int n = a.size();
        for (int l = 2, m = 1; l <= n; l <<= 1, m <<= 1) {
            for (int j = 0; j < n; j += l) for (int i = 0; i < m; i++) {
                if (!rev) add(a[i + j + m], a[i + j]);
                else sub(a[i + j + m], a[i + j]);
            }
        }
    }
    void FWTand(std::vector<int> &a, bool rev) {
        int n = a.size();
        for (int l = 2, m = 1; l <= n; l <<= 1, m <<= 1) {
            for (int j = 0; j < n; j += l) for (int i = 0; i < m; i++) {
                if (!rev) add(a[i + j], a[i + j + m]);
                else sub(a[i + j], a[i + j + m]);
            }
        }
    }
    void FWTxor(std::vector<int> &a, bool rev) {
        int n = a.size(), inv2 = (mod + 1) >> 1;
        for (int l = 2, m = 1; l <= n; l <<= 1, m <<= 1) {
            for (int j = 0; j < n; j += l) for (int i = 0; i < m; i++) {
                int x = a[i + j], y = a[i + j + m];
                if (!rev) {
                    a[i + j] = (x + y) % mod;
                    a[i + j + m] = (x - y + mod) % mod;
                } else {
                    a[i + j] = 1LL * (x + y) * inv2 % mod;
                    a[i + j + m] = 1LL * (x - y + mod) * inv2 % mod;
                }
            }
        }
    }
    std::vector<int> Or(std::vector<int> a1, std::vector<int> a2) {
        int n = std::max(a1.size(), a2.size()), N = extend(n);
        a1.resize(N), FWTor(a1, false);
        a2.resize(N), FWTor(a2, false);
        std::vector<int> A(N);
        for (int i = 0; i < N; i++) A[i] = 1LL * a1[i] * a2[i] % mod;
        FWTor(A, true);
        return A;
    }
    std::vector<int> And(std::vector<int> a1, std::vector<int> a2) {
        int n = std::max(a1.size(), a2.size()), N = extend(n);
        a1.resize(N), FWTand(a1, false);
        a2.resize(N), FWTand(a2, false);
        std::vector<int> A(N);
        for (int i = 0; i < N; i++) A[i] = 1LL * a1[i] * a2[i] % mod;
        FWTand(A, true);
        return A;
    }
    std::vector<int> Xor(std::vector<int> a1, std::vector<int> a2) {
        int n = std::max(a1.size(), a2.size()), N = extend(n);
        a1.resize(N), FWTxor(a1, false);
        a2.resize(N), FWTxor(a2, false);
        std::vector<int> A(N);
        for (int i = 0; i < N; i++) A[i] = 1LL * a1[i] * a2[i] % mod;
        FWTxor(A, true);
        return A;
    }
} fwt;
int pr[N/5+100],v[N+4],m=0;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0){
            pr[++m]=i;v[i]=m;
        }
        for(int j=1;j<=m;j++){
            if(j>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=j;
        }
    }
    vector<int>a{1},b(N+1);
    for(int i=1;i<=m;i++)
        b[pr[i]]=1;
    for(int m=M;m;m>>=1){
        if(m&1) a=fwt.Or(a,b);
        b=fwt.Or(b,b);
    }
    int ans=0;
    for(int i=1;i<=m;i++)
        ans=(ans+a[pr[i]])%mod;
    printf("%d\n",ans);
}

```