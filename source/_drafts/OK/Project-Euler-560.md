---
title: Project Euler 560
tags:
  - Project Euler
mathjax: true
---
<escape><!-- more --></escape>
    
# Project Euler 560
## 题目
### Coprime Nim


Coprime Nim is just like ordinary normal play Nim, but the players may only remove a number of stones from a pile  that is **coprime** with the current size of the pile. Two players remove stones in turn. The player who removes the last stone wins.

Let $L(n, k)$ be the number of **losing** starting positions for the first player, assuming perfect play, when the game is played with $k$ piles, each having between $1$ and $n - 1$ stones inclusively.

For example, $L(5, 2) = 6$ since the losing initial positions are $(1, 1), (2, 2), (2, 4), (3, 3), (4, 2)$ and $(4, 4)$.

You are also given $L(10, 5) = 9964, L(10, 10) = 472400303, L(10^3, 10^3)  \mod 1 000 000 007 = 954021836$.

Find $L(10^7, 10^7) \mod 1 000 000 007$




## 解决方案

```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100,M=100;
int sg[N+4];
bool mex[M+4];
int pr[N/10+100],v[N+4];
int main(){
    for(int i=1;i<=N;i++){
        memset(mex,0,sizeof(mex));
        for(int j=1;j<=i;j++)
            if(__gcd(i,j)==1) mex[sg[i-j]]=1;
        int j=0;
        for(;mex[j];++j);
        sg[i]=j;
        printf("%d %d\n",i,sg[i]);
    }
}

```

## 代码


```C++
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;

const int N=10000000;
const int M=10000000;
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
    v[1]=1;
    for(int i=2;i<=N;i+=2)
        v[i]=0;
    vector<int>a{1},b(m+1);
    for(int i=1;i<N;i++)
        ++b[v[i]];
    for(int m=M;m;m>>=1){
        if(m&1) a=fwt.Xor(a,b);
        b=fwt.Xor(b,b);
    }
    int ans=a[0];
    printf("%d\n",ans);
}

```