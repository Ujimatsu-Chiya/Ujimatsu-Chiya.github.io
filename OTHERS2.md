Q343

```
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=2e6;
//f(n)=n+1的最大质因数-1。
//n^3+1=(n+1)(n^2-n+1)
ll v1[N+4],b[N+4],v2[N+4];
int main(){
    for(int i=2;i<=N+1;i++){
        if(v1[i]==0){
            for(int j=i;j<=N+1;j+=i)
                v1[j]=i;
        }
    }
    for(int i=1;i<=N;i++)
        v1[i]=v1[i+1];
    for(int i=1;i<=N;i++)
        b[i]=1ll*i*i-i+1;
    for(int i=2;i<=N;i++){
        ll p=b[i];
        if(p==1) continue;
        for(ll j=i;j<=N;j+=p)
            while(b[j]%p==0)
                b[j]/=p,v2[j]=max(v2[j],p);
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        ans+=max(v1[i],v2[i])-1;
    printf("%lld\n",ans);
}

```

Q300

```
# include <bits/stdc++.h>
# define pi pair<int,int>
# define X first
# define Y second
# define lb(x) ((x) & -(x))
using namespace std;
typedef long long ll;
const int N=15;
int f[N+N+4][N+N+4];
int dx[4]={-1,1,0,0},dy[4]={0,0,-1,1};
int ans[1<<N];
//将每个接触面进行编码。z[i][j]表示第i个格子和第j个格子相邻。
//显而易见的是，如果第i个格子和第j个相邻，那么i和j不同奇偶性。
ll z[N][N];
int x[N*N],y[N*N];
unordered_set<ll>st;
void dfs(int fl,int px,int py,ll s){
    for(int i=0;i<4;i++){
        int nx=px+dx[i],ny=py+dy[i];
        if(f[nx][ny]!=-1){
            s|=1ll<<z[fl-1][f[nx][ny]];
        }
    }
    if(fl==N){
        st.insert(s);
        return;
    }
    for(int i=0;i<4;i++){
        int nx=px+dx[i],ny=py+dy[i];
        if(f[nx][ny]==-1){
            f[nx][ny]=fl;
            dfs(fl+1,nx,ny,s);
            f[nx][ny]=-1;
        }
    }

}
const int B=16,M=(1<<16)-1;
int bits[1<<B];
int calbits(ll x){
    int ans=0;
    for(;x;x>>=B)
        ans+=bits[x&M];
    return ans;
}
//计算出对应的分子。
int solve(){
    memset(f,-1,sizeof(f));
    if(N==1) return 1;
    int m=0;
    for(int i=0;i<N;i+=2)
        for(int j=1;j<N;j+=2){
            x[m]=i;y[m]=j;
            z[i][j]=z[j][i]=m++;
        }
    f[N][N]=0;f[N][N+1]=1;
    dfs(2,N,N+1,z[0][1]);
    int sum=0;
    for(int s=0;s<(1<<N);s++){
        int mx=0;
        ll y=0;
        for(int i=0;i<N;i+=2)
            for(int j=1;j<N;j+=2)
                if((s>>i&1)&&(s>>j&1))
                    y|=1ll<<z[i][j];
        for(ll x:st)
            mx=max(mx,calbits(x&y));
        sum+=mx;
    }
    return sum;
}
int main(){
    for(int i=0;i<(1<<B);i++)
        for(int j=0;j<B;j++)
            bits[i]+=i>>j&1;
    int fz=solve(),fm=1<<N;
    int g=__gcd(fz,fm);
    fz/=g;fm/=g;
    int pw2=log2(fm+1e-6);
    double ans=1.0*fz/fm;
    printf("%.*f\n",pw2,ans);
}

```

Q643

```
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const ll Q=1e11;
const ll mod=1000000007;
const int M = (int) sqrt(Q) * 2;
int phi[M+4],sphi[M+4];
unordered_map<ll,ll>mp;
ll inv(ll x,ll p){
    ll ans=1;
    for(int m=p-2;m;m>>=1){
        if(m&1) ans=ans*x%p;
        x=x*x%p;
    }
    return ans;
}
ll inv2= inv(2,mod);
ll sum_phi(ll x)
{
    if(x<=M)
        return sphi[x];
    if(mp.count(x))
        return mp[x];
    ll ans= ((x+1)%mod*(x%mod)%mod) * inv2 % mod;
    for(ll l=2,r;l<=x;l=r+1)
    {
        r= x / (x / l);
        ans= (ans - (r - l + 1) % mod * sum_phi(x / l) % mod + mod) % mod;
    }
    ans=(ans+mod)%mod;
    mp[x]=ans;
    return ans;
}
int main() {
    for (int i = 1; i <= M; i++)
        phi[i] = i;
    sphi[1] = 1;
    for (int i = 2; i <= M; i++) {
        if (phi[i] == i) {
            phi[i] = i - 1;
            for (int j = i + i; j <= M; j += i)
                phi[j] = phi[j] / i * (i - 1);
        }
        sphi[i] = (sphi[i - 1] + phi[i]) % mod;
    }
    ll ans=0;
    for(ll d=2;d<=Q;d<<=1)
        ans=(ans+sum_phi(Q/d)-1)%mod;
    printf("%lld\n",ans);

}
```

Q375

```
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
int Q=2e9,T;
const int A=290797,M=50515093;
//容易知道，S1到后面为一个循环数组，其中周期为T。
int S[M*3];
int l[M*3],r[M*3];
void gen(int m){
    stack<int>st;
    for(int i=0;i<m;i++){
        while(!st.empty() && S[i] < S[st.top()])
            st.pop();
        if(st.empty()) l[i]=0;
        else l[i]=st.top()+1;
        st.push(i);
    }
    while(!st.empty())
        st.pop();
    for(int i=m-1;i>=0;i--){
        while(!st.empty() && S[i] < S[st.top()])
            st.pop();
        if(st.empty()) r[i]=m-1;
        else r[i]=st.top()-1;
        st.push(i);
    }
}
ll solve(){
    //由于S数组是一个循环数组，故分类处理。
    int mn=*min_element(S, S + T);
    ll res=1ll*Q*(Q+1)/2,ans=0;
    if(Q<=T*2){
        for(int i=T;i<Q;i++)
            S[i]=S[i-T];
        gen(Q);
        for(int i=0;i<Q;i++){
            ll tp=1ll*(i-l[i]+1)*(r[i]-i+1);
            ans+=tp*S[i];
            res-=tp;
        }
        ans+=res*mn;
    }
    else{
        for(int i=0;i<T;i++)
            S[i+T]=S[i+T+T]=S[i];
        int block=Q/T,rest=Q%T;
        gen(2*T+rest);
        for(int i=0;i<T;i++){
            ll tp=1ll*(i-l[i]+1)*(r[i]-i+1);
            ans+=tp*S[i];
            res-=tp;
            int j=2*T+rest-1-i;
            tp=1ll*(j-l[j]+1)*(r[j]-j+1);
            ans+=tp*S[j];
            res-=tp;
            tp=1ll*(i+T-l[i+T]+1)*(r[i]-i+1);
            ll c=block-2+(i<rest);
            ans+=tp*S[i]*c;
            res-=tp*c;
        }
        ans+=res*mn;
    }
    return ans;
}
int main(){
    S[0]=1ll*A*A%M;
    for(int i=1;i<M;i++){
        S[i]=1ll*S[i-1]*S[i-1]%M;
        if(S[i]==S[0]){
            T=i;break;
        }
    }
    printf("%lld\n",solve());
}
```

Q709

```
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
// A000111
const int N=24680;
int mod=1020202009;
ll fac[N+4],finv[N+4],inv[N+4];
ll C(int n,int m){
    return 1ll*fac[n]*finv[m]%mod*finv[n-m]%mod;
}
ll f[N+4];
int main(){
    fac[0]=fac[1]=inv[0]=inv[1]=finv[0]=finv[1]=1;
    for(int i=2;i<=N;i++){
        fac[i]=fac[i-1]*i%mod;
        inv[i]=(mod-mod/i)*inv[mod%i]%mod;
        finv[i]=finv[i-1]*inv[i]%mod;
    }
    f[0]=f[1]=1;
    for(int n=1;n<N;n++){
        for(int k=0;k<=n;k+=2)
            f[n+1]=(f[n+1]+1ll*C(n,k)*f[k]%mod*f[n-k])%mod;
    }
    printf("%lld\n",f[N]);
}

```

Q479

```
N = 10**6
mod = 10 ** 9 + 7
# 原方程转化为k*x^3-k^2*x^2+x-k^3=0(x != 0)的解。
# 根据韦达定理，有x1+x2+x3=-b/a=k，x1x2+x2x3+x1x3=c/a=1/k，x1x2x3=-d/a。
# (ak+bk)(bk+ck)(ak+ck)=(ak+bk+ck)(akbk+bkck+ckak)-akbkck=1-k^2。
# 原式求解为(1-k^2)^p。

ans = 0
for k in range(2, N + 1):
    ans = (ans + (1 - k * k) * (pow(1 - k * k, N, mod) - 1) % mod * pow(1 - k * k - 1, mod - 2, mod)) % mod
ans = (ans % mod + mod) % mod
print(ans)

```

Q485

```
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=100000000,K=100000;
int f[N+4];
int main(){
    for(int i=1;i<=N;i++)
        f[i]=1;
    for(int i=2;i<=N;i++){
        if(f[i]!=1) continue;
        for(ll w=i,c=1;w<=N;w*=i,++c){
            for(int j=w;j<=N;j+=w){
                if(j/w%i==0) continue;
                f[j]*=(c+1);
            }
        }
    }
    ll ans=0;
    deque<int>q;
    for(int i=K,j=1;i<=N;i++){
        while(!q.empty()&&i-q.front()>=K) q.pop_front();
        for(;j<=i;j++){
            while(!q.empty()&&f[j]>=f[q.back()]) q.pop_back();
            q.push_back(j);
        }
        ans+=f[q.front()];
    }
    printf("%lld\n",ans);
}
```

Q510

```
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int Q=1e9;
//三个圆的半径满足1/sqrt(ra)+1/sqrt(rb)=1/sqrt(rc)
//rc=rarb/(ra+rb+2sqrt(rarb))，因此rarb必须是平方数。
//令ra=p^2(p+q)^2,rb=q^2(p+q)^2,rc=p^2q^2，其中p<=q，那么此时ra,rb,rc满足原方程。
//当gcd(p,q)=1时，这是一个本源三元组，可以知道，每个数乘以d仍然满足原方程。
int main(){
    ll ans=0;
    for(ll p=1;p*p*p*p<=Q;p++){
        for(ll q=p;q*q*(p+q)*(p+q)<=Q;q++){
            if(__gcd(p,q)!=1) continue;
            ll d=Q/(q*q*(p+q)*(p+q));
            ans+=(d+1)*d/2*(p*p*(p+q)*(p+q)+q*q*(p+q)*(p+q)+p*p*q*q);
        }
    }
    printf("%lld\n",ans);
}

```

Q506

```
from gmpy2 import is_prime

# A028355
# 发现，该序列的周期为15，第i个鼠是第i-15个数后面拼接一个固定的6位数。
# 将每个n分解成n=x*15+y再进行计算。

N = 10**14
mod = 123454321
inv1e6 = 96007682
m = 10 ** 6
a = [1, 2, 3, 4, 32, 123, 43, 2123, 432, 1234, 32123, 43212, 34321, 23432, 123432]
b = [234321, 343212, 432123, 321234, 123432, 432123, 212343, 432123, 123432, 321234, 432123, 343212, 234321, 123432, 123432]
T = 15
ans = 0
for i in range(T):
    cnt = N // T + (i < N % T)
    c1 = (pow(m, cnt, mod) - 1) * inv1e6 % mod
    c2 = (c1 - cnt + mod) * inv1e6 % mod
    ans = (ans + a[i] * c1 + b[i] * c2) % mod
print(ans)

```

Q609

```
#include <bits/stdc++.h>
typedef long long ll;
using namespace std;
const int N=100000000;
int s[N+4];
int v[N+4],pr[N+4],m=0;
int cnt[N+4];
ll mod=1e9+7;
int main(){
    for(int i=2;i<=N;i++){
        if(v[i]==0) v[i]=i,pr[++m]=i;
        for(int j=1;j<=m;j++){
            if(pr[j]>v[i]||pr[j]>N/i) break;
            v[i*pr[j]]=pr[j];
        }
        s[i]=s[i-1]+(v[i]==i);
    }
    v[0]=-1;
    for(int i=1;i<=N;i++){
        for(int j=i,cs=0,cp=0;j;j=s[j]){
            ++cs;
            if(v[j]!=j) ++cp;
            if(cs>=2) ++cnt[cp];
            if(j==1) break;
        }
    }
    ll ans=1;
    for(int j=0;j<=N;j++)
        if(cnt[j]>0) ans=ans*cnt[j]%mod;
    printf("%lld\n",ans);
}

```

Q706

```
# include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=100000;
ll f[N+4][3][3][3][3],mod=1e9+7;
/*
数字串的前缀和为s[0]~s[n]
f[m][i][j][k][l]表示前m+1个值s[0]~s[m]中，有
 s[?]%3==1的个数 % 3 = i
 s[?]%3==2的个数 % 3 = j
 s[m]%3==k
 已经有的非空子串数目 % 3 = l.
 */
void add(ll &x,ll y){
    x=(x+y)%mod;
}

int main(){
    f[1][0][0][0][1] = 3;
    f[1][1][0][1][0] = 3;
    f[1][0][1][2][0] = 3;
    for(int m=1;m<N;m++)
        for(int i=0;i<3;i++)
            for(int j=0;j<3;j++)
                for(int k=0;k<3;k++)
                    for(int l=0;l<3;l++){
                        //0~m中一共有m+1个值。
                        int c0=(m+1-i-j+6)%3;
                        ll &now = f[m][i][j][k][l];
                        if(now == 0)
                            continue;
                        if(k==0){
                            add(f[m+1][i][j][k][(l+c0)%3],now*4); //0,3,6,9
                            add(f[m+1][(i+1)%3][j][(k+1)%3][(l+i)%3],now*3);//1,4,7
                            add(f[m+1][i][(j+1)%3][(k+2)%3][(l+j)%3],now*3);//2,5,8
                        }
                        else if(k==1){
                            add(f[m+1][(i+1)%3][j][k][(l+i)%3],now*4);//0,3,6,9
                            add(f[m+1][i][(j+1)%3][(k+1)%3][(l+j)%3],now*3);// 1,4,7
                            add(f[m+1][i][j][(k+2)%3][(l+c0)%3],now*3);//2,5,8
                        }
                        else{
                            add(f[m+1][i][(j+1)%3][k][(l+j)%3],now*4);//0,3,6,9
                            add(f[m+1][i][j][(k+1)%3][(l+c0)%3],now*3);//1,4,7
                            add(f[m+1][(i+1)%3][j][(k+2)%3][(l+i)%3],now*3);//2,5,8
                        }
                    }
    ll ans=0;
    for(int i=0;i<3;i++)
        for(int j=0;j<3;j++)
            for(int k=0;k<3;k++)
                add(ans,f[N][i][j][k][0]);
    printf("%lld\n",ans);
}

```

Q501

```
#include <bits/stdc++.h>
using namespace std;
typedef long long ll;
const ll Q = 1000000000000;
const ll M = pow(Q,2.0/3) + 2;


char vis[M + 1];
int sum[M + 1],pr[M + 1],m;

unordered_map<ll,ll> mp,mq;
ll g(ll x, ll a) {
    if (a == 1 || x == 0)return (x + 1) / 2;
    ll &v = mp[(x << 10) + a];
    if (v)return v;
    return v = g(x, a - 1) - g(x / pr[a], a - 1);
}
ll cal(ll n) {
    if (n <= M)return sum[n];
    ll &v = mq[n];
    if (v) return v;
    ll a = cal(pow(n, 1.0 / 4));
    ll b = cal(sqrt(n));
    ll c = cal(pow(n, 1.0 / 3));
    ll s = g(n, a) + (b + a - 2) * (b - a + 1) / 2;
    for (ll i = a + 1; i <= b; i++) {
        ll w = n / pr[i];
        s -= cal(w);
        ll csqw = cal(sqrt(w));
        if (i <= c) {
            for (ll j = i; j <= csqw; j++)
                s += j - 1 - cal(w / pr[j]);
        }
    }
    return v = s;
}
int main() {
    ll ans = 0;
    for (ll i = 2; i <= M; i++) {
        if (!vis[i]) {
            for (ll j = i * i; j <= M; j += i) vis[j] = 1;
            pr[++m] = i;
        }
        sum[i] = m;
    }
    for (ll i = 1; i <= m && pr[i] <= pow(Q, 1.0 / 7); i++)
        ans++;
    ll tmp;
    for (int i = 1; i <= m && (tmp = Q / (1ll * pr[i] * pr[i] * pr[i])) >= 2; i++) {
        ans += cal(tmp) - (tmp >= pr[i]);
    }
    for (ll i = 1; 1ll * pr[i] * pr[i] * pr[i] <= Q; i++)
        for (ll j = i + 1; j <= m && pr[j + 1] <= (tmp = Q / (1ll * pr[i] * pr[j])); j++)
            ans += cal(tmp) - cal(pr[j]);
    printf("%lld\n", ans);
    return 0;
}
```

Q581

```
# include <bits/stdc++.h>
using namespace std;
const int M=47;
int pr[M+4],m=0,b[M+4];
typedef long long ll;
int main(){
    ll N=2e12;
    for(int i=2;i<=M;i++){
        if(b[i]) continue;
        pr[++m]=i;
        for(int j=i+i;j<=M;j+=i)
            b[j]=1;
    }
    priority_queue<ll,vector<ll>,greater<ll>>q;
    q.push(1);
    ll ans=0,pre=1;
    while(!q.empty()){
        ll u=q.top();q.pop();
        if(u==pre+1){
            ans+=pre;
        }
        pre=u;
        for(int i=1;i<=m;i++){
            ll v=u*pr[i];
            if(v>N) break;
            q.push(v);
            if(u%pr[i]==0) break;
        }
    }
    printf("%lld\n",ans);
}

```

Q713

```
# A134546
for N in range(2, 11):
    ans = 0
    for r in range(1, N):
        q, s = divmod(N, r)
        ans += r * q * (q - 1) // 2 + s * q
        print(N, r, r * q * (q - 1) // 2 + s * q)

for n in range(2, 11):
    for k in range(2, n):
        m = n // k
        print(n, k, (n - m) * (n - m - 1) // 2 + (k - 1) * (m + 1) * m // 2)

'''
Fleshing out the explanation - thinking of the N fuses as nodes, after some number of tries we can construct the graph G
 in which two nodes (fuses) are adjacent if and only if they have not been tested together. A strategy is guaranteed to
  succeed if and only if G contains no clique of size m. The optimal strategy minimizes the number of tries, or 
  equivalently maximizes the number of edges in G. So we are looking for the graph with the maximum number of edges that 
  contains no clique of size m. By Turan's Theorem, this is the Turan graph T(n,m-1). The optimal strategy is then defined 
  by partitioning the N nodes into m-1 subsets of as equal size as possible, and testing each pair within each subset.
'''

```

Q733

```
# include <bits/stdc++.h>
# define mem(a,b) memset(a,b,sizeof(a))
# define lb(x) ((x)&-(x))
typedef long long ll;
using namespace std;
const int N=1000000;
int a[N+4],b[N+4],m;
ll f1[N+4],f2[N+4],s1[N+4],s2[N+4],mod=1e9+7;
void add(ll *s,int p,ll x){
    for(int i=p;i<=m;i+=lb(i))
        s[i]=(s[i]+x)%mod;
}
ll que(ll *s,int p){
    ll ans=0;
    for(int i=p;i;i-=lb(i))
        ans=(ans+s[i])%mod;
    return ans;
}
int main(){
    a[1]=153;
    for(int i=2;i<=N;i++)
        a[i]=a[i-1]*153%10000019;
    for(int i=1;i<=N;i++)
        b[i]=f2[i]=a[i],f1[i]=1;
    sort(b+1,b+N+1);
    m=unique(b+1,b+N+1)-b-1;
    for(int i=2;i<=4;i++){
        mem(s1,0);
        mem(s2,0);
        for(int j=1;j<=m;j++){
            int p=lower_bound(b+1,b+m+1,a[j])-b;
            ll q1=que(s1,p-1),q2=que(s2,p-1);
            add(s1,p,f1[j]);
            add(s2,p,f2[j]);
            f1[j]=q1;f2[j]=(q2+q1*a[j])%mod;
        }
    }
    ll ans=0;
    for(int i=1;i<=N;i++)
        ans=(ans+f2[i])%mod;
    printf("%lld\n",ans);
}

```

Q618

```
# include <bits/stdc++.h>
# define mem(a,b) memset(a,b,sizeof(a))
# define lb(x) ((x)&-(x))
typedef long long ll;
using namespace std;
const int N=100000,Q=24;
bool b[N+4];
int pr[N+4],m=0;
int que[144],p=0;
ll f[N+4],mod=1e9;
int main(){
    for(int i=1,a=1,b=2;i<Q;i++){
        que[++p]=a;
        int c=a+b;
        a=b;b=c;
    }
    int mx=que[p];
    for(int i=2;i<=mx;i++){
        if(b[i]) continue;
        pr[++m]=i;
        for(int j=i+i;j<=mx;j+=i)
            b[j]=1;
    }
    f[0]=1;
    for(int i=1;i<=m;i++)
        for(int j=pr[i];j<=mx;j++)
            f[j]=(f[j]+f[j-pr[i]]*pr[i])%mod;
    ll ans=0;
    for(int i=1;i<=p;i++)
        ans=(ans+f[que[i]])%mod;
    printf("%lld\n",ans);
}

```

Q353

```
# include <bits/stdc++.h>
using namespace std;
const int N=100000,M=15;
typedef long long ll;
double pi=acos(-1.0);
bool vis[N+4];
ll x[N+4],y[N+4],z[N+4],r,m;
double d[N+4];
void add(int i,int j,int k){
    x[++m]=i;y[m]=j;z[m]=k;
    if(i>0){
        x[++m]=-i;y[m]=j;z[m]=k;
    }
}
double dis(int i,int j){
    ll v=x[i]*x[j]+max(y[i]*y[j]+z[i]*z[j],y[i]*z[j]+z[i]*y[j]);
    return pow(acos(1.0*v/r/r),2);
}
double solve(ll r){
    m=0;::r=r;
    for(ll i=0;i*i<=r*r;i++)
    for(ll j=i;i*i+j*j<=r*r;j++){
        ll k=sqrt(r*r-i*i-j*j+1e-10);
        if(i*i+j*j+k*k!=r*r) continue;
        if(k<j) break;
        add(i,j,k);
        if(i!=j) add(j,i,k);
        if(j!=k) add(k,i,j);
    }
    memset(vis,0,sizeof(vis));
    for(int i=1;i<=m;i++)
        d[i]=(x[i]==-r?0:1e100);
    int p;
    for(;;){
        p=0;
        for(int i=1;i<=m;i++){
            if(vis[i]) continue;
            if(p==0||d[i]<d[p]) p=i;
        }
        if(x[p]==r) break;
        vis[p]=1;
        for(int j=1;j<=m;j++)
            if(!vis[j])
                d[j]=min(d[j],d[p]+dis(p,j));
    }
    return d[p]/pi/pi;
}
int main(){
    double ans=0;
    for(int i=1;i<=M;i++){
        ans+=solve((1<<i)-1);
    }
    printf("%.10f\n",ans);
}

```

Q353

```
# include <bits/stdc++.h>
using namespace std;
const int N=100000,M=15;
typedef long long ll;
double pi=acos(-1.0);
bool vis[N+4];
ll x[N+4],y[N+4],z[N+4],r,m;
double d[N+4];
void add(int i,int j,int k){
    x[++m]=i;y[m]=j;z[m]=k;
    if(i>0){
        x[++m]=-i;y[m]=j;z[m]=k;
    }
}
double dis(int i,int j){
    ll v=x[i]*x[j]+max(y[i]*y[j]+z[i]*z[j],y[i]*z[j]+z[i]*y[j]);
    return pow(acos(1.0*v/r/r),2);
}
double solve(ll r){
    m=0;::r=r;
    for(ll i=0;i*i<=r*r;i++)
    for(ll j=i;i*i+j*j<=r*r;j++){
        ll k=sqrt(r*r-i*i-j*j+1e-10);
        if(i*i+j*j+k*k!=r*r) continue;
        if(k<j) break;
        add(i,j,k);
        if(i!=j) add(j,i,k);
        if(j!=k) add(k,i,j);
    }
    memset(vis,0,sizeof(vis));
    for(int i=1;i<=m;i++)
        d[i]=(x[i]==-r?0:1e100);
    int p;
    for(;;){
        p=0;
        for(int i=1;i<=m;i++){
            if(vis[i]) continue;
            if(p==0||d[i]<d[p]) p=i;
        }
        if(x[p]==r) break;
        vis[p]=1;
        for(int j=1;j<=m;j++)
            if(!vis[j])
                d[j]=min(d[j],d[p]+dis(p,j));
    }
    return d[p]/pi/pi;
}
int main(){
    double ans=0;
    for(int i=1;i<=M;i++){
        ans+=solve((1<<i)-1);
    }
    printf("%.10f\n",ans);
}

```

Q724

```
# include <bits/stdc++.h>
using namespace std;
/*
https://en.wikipedia.org/wiki/Coupon_collector%27s_problem#Solution
E[tx]表示持有x张票时持续的时间的期望。
tx~E(n/(n-x+1))
E[C]=E[t1]+E[t2]+...+E[tn]=n*H(n)
D[C]=D[t1]+D[t2]+...+D[tn]=n^2(1+1/4+...+1/n^2)。
E[C^2]=E[C]^2+D[C]。
从整体上看，每次都会有一个无人机被添加速度，因此第i秒的操作在前n秒就贡献了n-i+1的距离。
因此答案为E[C(C+1)/2]。
平均下来就是一台无人机可以飞E[C(C+1)/2]/n。
*/
const int N=1e8;
int main(){
    double ec=0,dc=0;
    for(int i=1;i<=N;i++){
        double p=1.0*(N-i+1)/N;
        ec+=1.0/p;
        dc+=(1.0-p)/p/p;
    }
    double ec2=ec*ec+dc;
    double ans=0.5*(ec+ec2)/N;
    printf("%.f\n",ans);
}

```

Q294

```
# include <bits/stdc++.h>
# define mem(a,b) memset(a,b,sizeof(a))
using namespace std;
typedef long long ll;
const ll N=3138428376721;
const int M=23*24;
ll a[M],b[M][M],mod=1e9;
ll c[M][M]={0};
void mul_self(ll b[M][M]){
    mem(c,0);
    for(int i=0;i<M;i++)
        for(int k=0;k<M;k++)
            for(int j=0;j<M;j++)
                c[i][j]=(c[i][j]+b[i][k]*b[k][j])%mod;
    memcpy(b,c,sizeof(c));
}
void mul(ll a[M],ll b[M][M]){
    ll c[M]={0};
    for(int i=0;i<M;i++)
        for(int k=0;k<M;k++)
            c[i]=(c[i]+a[k]*b[k][i])%mod;
    memcpy(a,c,sizeof(c));

}
int enc[23][24],m=0;
int main(){
    for(int i=0;i<23;i++)
        for(int j=0;j<24;j++)
            enc[i][j]=m++;
    for(int i=0;i<10;i++)
        a[enc[i][i]]=1;
    for(int i=0;i<23;i++)
        for(int j=0;j<24;j++)
            for(int k=0;k<10&&j+k<24;k++){
                b[enc[i][j]][enc[(i*10+k)%23][j+k]]=1;
            }
    for(ll m=N-1;m;m>>=1){
        if(m&1) mul(a,b);
        mul_self(b);
    }
    ll ans=a[enc[0][23]];
    printf("%lld\n",ans);
}
//todo Thread

```

Q731

```
N = 10 ** 16
'''
模拟除法。
如果需要计算1/k的后面第n位小数，那么就是计算10^(n-1)/k后面的第1位小数。
根据题目要求，这题并不关心除k之后的整数部分。
另外(10^(n-1)%k)/k和10^(n-1)/k的小数部分相同。
'''
f = 0
i = 0
while True:
    if N < 3 ** i + 1:
        break
    f += pow(10, N - 3 ** i - 1, 3 ** i) / 3 ** i
    f -= int(f)
    i += 1
ans = str(f)[2:][:10]
print(ans)

```

Q727

```
# include <bits/stdc++.h>
# define mem(a,b) memset(a,b,sizeof(a))
using namespace std;
typedef long long ll;
const int N=100;

tuple<double,double,double> normalize(tuple<double,double,double> P){
    double s=get<0>(P)+get<1>(P)+get<2>(P);
    return make_tuple(get<0>(P)/s,get<1>(P)/s,get<2>(P)/s);
}
/*
D: 内心
E：Equal detour point，三角形内一点P满足|AP|+|BP|-|AB|=|AP|+|CP|-|AC|=|BP|+|CP|-|BC|
在重心坐标系下表示。
重心坐标系下两点距离计算向量PQ的长度|PQ|：|PQ|^2=-a^2yz-b^2zx-c^2xy
*/
int main(){
    double ans=0,a1,b1,c1,a2,b2,c2;
    int cnt=0;
    for(int ra=1;ra<=N;ra++)
    for(int rb=ra+1;rb<=N;rb++){
        int g=__gcd(ra,rb);
        for(int rc=rb+1;rc<=N;rc++){
            if(__gcd(g,rc)!=1) continue;
            double a=ra+rb,b=rb+rc,c=rc+ra;
            double p=(a+b+c)*0.5;
            double S=sqrt(p*(p-a)*(p-b)*(p-c));
            auto D=make_tuple(a,b,c);
            auto E=make_tuple(a+S/(p-a),b+S/(p-b),c+S/(p-c));
            tie(a1,b1,c1)=normalize(D);
            tie(a2,b2,c2)=normalize(E);
            double x=a2-a1,y=b2-b1,z=c2-c1;
            double de2=-a*a*y*z-b*b*z*x-c*c*x*y;
            ++cnt;
            ans+=sqrt(de2);
        }
    }
    ans/=cnt;
    printf("%.8f\n",ans);
}

```

Q395

```
# include <bits/stdc++.h>
using namespace std;
const double eps = 1e-15;
double minx = 0, miny = 0, maxx = 1, maxy = 1;
double leftRotate = acos(0.8);
//直接将正方形的下边旋转约180-53度。
double rightRotate = -acos(0.6);
double tag = 5;
struct Square {
    double len, x, y, rad;
};

int main() {

    queue<Square> q;
    q.push({1, 0, 0, 0});
    while (!q.empty()) {
        Square prm = q.front();q.pop();
        //正方形左下角的点。
        double len = prm.len, ldx = prm.x, ldy = prm.y, rad = prm.rad;

        minx = min(minx, ldx);
        maxx = max(maxx, ldx);
        miny = min(miny, ldy);
        maxy = max(maxy, ldy);

        double cosrad = cos(rad);
        double sinrad = sin(rad);
        double dx = len * cosrad;
        double dy = len * sinrad;
        //正方形左上角的点。
        double lux = ldx - dy, luy = ldy + dx;
        //正方形位于上边上面的新点。
        double tx = lux + ((dx * 0.8) - (dy * 0.6)) * 0.8,ty = luy + ((dx * 0.6) + (dy * 0.8)) * 0.8;

        if (len * 0.8 > eps) {
            double pl = len * tag * 0.8;
            if (lux > maxx - pl || lux < minx + pl || luy > maxy - pl || luy < miny + pl) {
                q.push({len * 0.8, lux, luy, rad + leftRotate});
            }

            if (len * 0.6 > eps) {
                pl = len * tag * 0.6;
                if (tx > maxx - pl || tx < minx + pl || ty > maxy - pl || ty < miny + pl) {
                    q.push({len * 0.6, tx, ty, rad + rightRotate});
                }
            }
        }
    }
    double ans = (maxx - minx) * (maxy - miny);
    printf("%.10f\n", ans);
}