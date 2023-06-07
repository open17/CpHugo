---
title: 数据结构学习合集
slug: DSall
date: 2023-06-04 00:00:00+0000
categories:
    - DS
---
## 单调栈
### 模板1
- 这种思路通常用于寻找右边的数（求左边时倒叙即可）
- 每次stack弹出时才记录答案，因此需要维护一个数组或者哈希表
- 确定单调性与目标相反即可，若求右最小，单调增（方向指的是自底向顶，后面同），最大反之即可
- 这里以求右边NGE为代表
```cpp
const int N=3e6+3;
int a[N],b[N];
void NGE(int n){
    stack<int> s;
    FOR(i,1,n+1){
        while(!s.empty()&&a[s.top()]<a[i]){
            b[s.top()]=i;
            s.pop();
        }
        s.push(i);
    }
}
```
### 模板2
- 这种思路通常用于寻找左边的数
- 寻找右边时，应反转列表（实际上倒叙即可）来看
- 这种写法每次维护后的栈顶即使答案
- 这里以求右边NGE为代表
```cpp
const int N=3e6+3;
int a[N],b[N];
void NGE(int n){
    stack<int> s;
    for(int i=n;i>0;i--){
        //这里的等号要注意，不然如 5，5 的话返回的是 2，0（下标从1开始）
        while(!s.empty()&&a[s.top()]<=a[i]){
            s.pop();
        }
        if(!s.empty()){
            b[i]=s.top();
        }
        s.push(i);
    }
}
```
### 补充
常用技巧：哨兵节点          
还要我发现我总结的上面的两个模板,灵神有个更本质的解释:https://leetcode.cn/problems/next-greater-node-in-linked-list/solution/tu-jie-dan-diao-zhan-liang-chong-fang-fa-v9ab/        
### 练习
#### 传统单调栈系列
```cpp
//https://leetcode.cn/problems/next-greater-element-i/
//哈希+NGE
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        stack<int> a;
        map<int,int> m;
        vector<int> ans;
        for(int i=0;i<nums1.size();i++){
            m[nums1[i]]=i;
            ans.push_back(-1);
        }
        //max=1e4
        a.push(1e4+1);
        for(auto i:nums2){
            while(a.top()<i){
                int x=a.top();
                a.pop();
                if(m.count(x)){
                    ans[m[x]]=i;
                }
            }
            a.push(i);
        }
        return ans;
    }
};
//https://leetcode.cn/problems/next-greater-element-ii/
//成环数组+NGE
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        stack<int> a;
        int s=nums.size();
        vector<int> ans(s,-1);
        nums.push_back(1e9+1);
        a.push(s);
        for(int i=0;i<2*s-1;i++){
            while(nums[a.top()]<nums[i%s]){
                ans[a.top()]=nums[i%s];
                a.pop();
            }
            a.push(i%s);
        }
        return ans;
    }
};

```
## ST表
### 练习
```cpp
//https://codeforces.com/problemset/problem/1709/D
//正确理解题意->贪心思考->转换成RMQ问题->ST表
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define For(w, a, n) for(int w=(a);w<(n);++w)
#define _For(a,b,c) for(int a=(b);a>(c);a--)
#define all(x) (x).begin(),x.end()
#define inf 0x3f3f3f3f
//对拍
#define fo1 freopen("data.in","r",stdin);freopen("res.out","w",stdout);
#define fo2 freopen("data.in","r",stdin);freopen("ans.out","w",stdout);
//输出数组
#define printA(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> pii;
const int N=3e6;
const int MOD=1e9+7;
inline int read() {
    int x = 0, f = 1;
    char ch = getchar();
    while (ch < '0' || ch > '9') {
        if (ch == '-')
            f = -1;
        ch = getchar();
    }
    while (ch >= '0' && ch <= '9') {
        x = x * 10 + ch - '0';
        ch = getchar();
    }
    return x * f;
}
inline void write(int x)
{
    if (x < 0) { putchar('-'); x = -x; }
    if (x > 9) write(x / 10);
    putchar(x % 10 + '0');
}
const int MAXN = 2e5 + 5;   // 最大数组长度
const int MAXK = ceil(log2(MAXN));        // log2(MAXN) 向上取整
int a[MAXN];                // 输入数组
int st[MAXN][MAXK + 1];     // ST表
int Log2[MAXN];
void build(int n) {
    for (int i = 1; i <= n; i++) {
        st[i][0] = a[i];    // 初始化第一列
    }
    for (int j = 1; j <= MAXK; j++) {
        for (int i = 1; i + (1 << j) - 1 <= n; i++) {
            st[i][j] = max(st[i][j - 1], st[i + (1 << (j - 1))][j - 1]); // 更新ST表
        }
    }
    for (int i = 2; i <= n; ++i) Log2[i] = Log2[i / 2] + 1;
}

int query(int l, int r) {
    if (l > r) swap(l, r);
    int k = Log2[r - l + 1]; // 计算区间长度的对数，向下取整
    return max(st[l][k], st[r - (1 << k) + 1][k]); // 返回区间最小值
}

int n,m;
inline void hhhh(){
    //todo
    int xs,ys,xe,ye,k;
    xs=read();
    ys=read();
    xe=read();
    ye=read();
    k=read();
    // cout<<query(ys,ye)<<" "<<(n-xs)/k*k+xs-1<<endl;
    if (xs%k!=xe%k||ys%k!=ye%k){
		cout<<"NO"<<'\n';
	}
	else if(query(ys,ye)>((n-xs)/k*k+xs-1)){
	    cout<<"NO"<<'\n';
	}
	else{
	    cout<<"YES"<<'\n';
	}
}

int main() {
    n=read();
    m=read();
    For(i,1,m+1)a[i]=read();
    build(m);
    int T;
    T=read();
    while(T--){
        hhhh();
    }
    return 0;
}
```
## DSU
### 练习
#### 普通并查集
```cpp
// https://codeforces.com/problemset/problem/1411/C
// 思维转换->成环判断
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define For(w, a, n) for(int w=(a);w<(n);++w)
#define _For(a,b,c) for(int a=(b);a>(c);a--)
#define all(x) (x).begin(),x.end()
#define inf 0x3f3f3f3f
//对拍
#define fo1 freopen("data.in","r",stdin);freopen("res.out","w",stdout);
#define fo2 freopen("data.in","r",stdin);freopen("ans.out","w",stdout);
//输出数组
#define printA(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> pii;
const int N=1e5+5;
const int MOD=1e9+7;
inline int read() {
    int x = 0, f = 1;
    char ch = getchar();
    while (ch < '0' || ch > '9') {
        if (ch == '-')
            f = -1;
        ch = getchar();
    }
    while (ch >= '0' && ch <= '9') {
        x = x * 10 + ch - '0';
        ch = getchar();
    }
    return x * f;
}
inline void write(int x)
{
    if (x < 0) { putchar('-'); x = -x; }
    if (x > 9) write(x / 10);
    putchar(x % 10 + '0');
}

int root[N];
int ranks[N];
int find(int x) {
    if (x == root[x]) {
        return x;
    }
    return root[x] = find(root[x]);
}
void unionSet(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);
    if (rootX != rootY) {
        if (ranks[rootX] > ranks[rootY]) {
            root[rootY] = rootX;
        } else if (ranks[rootX] < ranks[rootY]) {
            root[rootX] = rootY;
        } else {
            root[rootY] = rootX;
            ranks[rootX] += 1;
        }
    }
}
bool connected(int x, int y) {
    return find(x) == find(y);
}

inline void hhhh(){
    int n=read();
    int m=read();
    For(i,0,n+2){
        root[i]=i;
        ranks[i]=1;
    }
    int cnt=0;
    For(i,0,m){
        int x=read(),y=read();
        if(x!=y){
            cnt++;
            if(connected(x,y))cnt++;
            else unionSet(x,y);
        }
    }
    write(cnt);
    cout<<'\n';
}

int main() {
    //hhhh();
    int T;
    T=read();
    while(T--){
        hhhh();
    }
    return 0;
}
// https://codeforces.com/problemset/problem/371/D
// 先写出直接模拟,然后思考如何优化过程->并查集优化
#include<bits/stdc++.h>
using namespace std;
// #define int long long
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define For(w, a, n) for(int w=(a);w<(n);++w)
#define _For(a,b,c) for(int a=(b);a>(c);a--)
#define all(x) (x).begin(),x.end()
#define inf 0x3f3f3f3f
//对拍
#define fo1 freopen("data.in","r",stdin);freopen("res.out","w",stdout);
#define fo2 freopen("data.in","r",stdin);freopen("ans.out","w",stdout);
//输出数组
#define printA(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> pii;
const int N=2e5+5;
const int MOD=1e9+7;
inline int read() {
    int x = 0, f = 1;
    char ch = getchar();
    while (ch < '0' || ch > '9') {
        if (ch == '-')
            f = -1;
        ch = getchar();
    }
    while (ch >= '0' && ch <= '9') {
        x = x * 10 + ch - '0';
        ch = getchar();
    }
    return x * f;
}
inline void write(int x)
{
    if (x < 0) { putchar('-'); x = -x; }
    if (x > 9) write(x / 10);
    putchar(x % 10 + '0');
}

int a[N];//体积
int b[N];//水
ll root[N];
void initbuf(ll n){
    for (ll i = 0; i <= n; i++) {
        root[i] = i;
    }
}
ll find(ll x) {
    if (x == root[x]) {
        return x;
    }
    return root[x] = find(root[x]);
}
void unionSet(ll x, ll y) {
    ll rootX = find(x);
    ll rootY = find(y);
    root[rootY] = rootX;
}
bool connected(ll x, ll y) {
    return find(x) == find(y);
}
inline void hhhh(){
    int n=read();
    For(i,1,n+1)a[i]=read();
    initbuf(n);
    int m=read();
    while(m--){
        int num=read();
        if(num==1){
            int p=read();
            int x=read();
            int i=find(p);
            while(i<=n&&b[i]+x>=a[i]){
                x-=a[i]-b[i];
                b[i]=a[i];
                if(p!=i)unionSet(i,i-1);
                i++;
            }
            if(i<=n){
                if(p!=i)unionSet(i,i-1);
                b[i]+=x;
            }
        } 
        else{
            write(b[read()]);
            cout<<'\n';
        }
    }
    
}
signed main() {
    hhhh();
    return 0;
}
```
## 分块
### 练习
```cpp
// https://codeforces.com/problemset/problem/103/D
// 要维护区间离散的点用什么数据结构优化??线段树,树状数组不合适->优雅暴力:分块
// DP/暴力    根号区分
#include<bits/stdc++.h>
using namespace std;
#define int long long
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define For(w, a, n) for(int w=(a);w<(n);++w)
#define _For(a,b,c) for(int a=(b);a>(c);a--)
#define all(x) (x).begin(),x.end()
#define inf 0x3f3f3f3f
//对拍
#define fo1 freopen("data.in","r",stdin);freopen("res.out","w",stdout);
#define fo2 freopen("data.in","r",stdin);freopen("ans.out","w",stdout);
//输出数组
#define printA(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> pii;
const int N=3e5+5;
const int MOD=1e9+7;
inline int read() {
    int x = 0, f = 1;
    char ch = getchar();
    while (ch < '0' || ch > '9') {
        if (ch == '-')
            f = -1;
        ch = getchar();
    }
    while (ch >= '0' && ch <= '9') {
        x = x * 10 + ch - '0';
        ch = getchar();
    }
    return x * f;
}
inline void write(int x)
{
    if (x < 0) { putchar('-'); x = -x; }
    if (x > 9) write(x / 10);
    putchar(x % 10 + '0');
}

int w[N];
int ans[N];
int n;
int x;
vector<pii> hashA[N];
int dp[N*2];
inline void hhhh(){
    int p=read();
    // cout<<p<<'\n';
    For(i,0,p){
        int a=read(),b=read();
        if(b>x){
            int res=0;
            for(int j=a;j<=n;j+=b){
                res+=w[j];
            }
            ans[i]=res;
        }
        else{
            hashA[b].push_back(make_pair(a,i));
        }
    }
    For(i,1,x+1){
        if(hashA[i].size()){
            _For(j,n,0) dp[j]=dp[j+i]+w[j];
            For(k,0,hashA[i].size()){
                ans[hashA[i][k].second]=dp[hashA[i][k].first];
            }
            memset(dp,0,sizeof dp);
        }
    }
    For(i,0,p){
        cout<<ans[i]<<'\n';
    }
}
signed main() {
    n=read();
    x=sqrt(n);
    For(i,1,n+1)w[i]=read();
    hhhh();
    return 0;
}
```
## 线段树
### 练习
```cpp
// https://codeforces.com/problemset/problem/339/D
//虽然是单点修改和区间查询,但是因为要分奇数偶数层,所以不方便用树状数组
#include<bits/stdc++.h>
using namespace std;
// #define int long long
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define For(w, a, n) for(int w=(a);w<(n);++w)
#define _For(a,b,c) for(int a=(b);a>(c);a--)
#define all(x) (x).begin(),x.end()
#define inf 0x3f3f3f3f
//对拍
#define fo1 freopen("data.in","r",stdin);freopen("res.out","w",stdout);
#define fo2 freopen("data.in","r",stdin);freopen("ans.out","w",stdout);
//输出数组
#define printA(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> pii;
const int N=2e5+5;
const int MOD=1e9+7;
inline int read() {
    int x = 0, f = 1;
    char ch = getchar();
    while (ch < '0' || ch > '9') {
        if (ch == '-')
            f = -1;
        ch = getchar();
    }
    while (ch >= '0' && ch <= '9') {
        x = x * 10 + ch - '0';
        ch = getchar();
    }
    return x * f;
}
inline void write(int x)
{
    if (x < 0) { putchar('-'); x = -x; }
    if (x > 9) write(x / 10);
    putchar(x % 10 + '0');
}
const int MAXN=(1<<17)+9;
//开4倍
//n 为维护的数组长度，A为维护的数组
ll tree[MAXN << 2], n,A[MAXN];
int flag=1;
void push_up(int p){
    //这里维护的是区间和
    if(flag==1){
        tree[p] = tree[p << 1]|tree[p << 1 | 1];
    }
    else{
        tree[p] = tree[p << 1]^tree[p << 1 | 1];
    }
    flag^=1;
}
void build(int p = 1, int cl = 1, int cr = n)
{
    //如果叶子节点
    if (cl == cr) {
        tree[p] = A[cl];
        flag=1;
        return;   
    }
    //左右递归建树
    int mid = (cl + cr) >> 1;
    build(p << 1, cl, mid);
    build(p << 1 | 1, mid + 1, cr);
    push_up(p);
}
void update(int l, int r, int d, int p = 1, int cl = 1, int cr = n)
{
    if (cl >= l && cr <= r){
        tree[p]=d * (cr - cl + 1);
        flag=1;
        return;
    }
    int mid = (cl + cr) >> 1;
    if (mid >= l) update(l, r, d, p << 1, cl, mid);
    if (mid < r) update(l, r, d, p << 1 | 1, mid + 1, cr);
    push_up(p);
}

inline void hhhh(){
    int x=read(),m=read();
    n=1<<x;
    For(i,1,n+1)A[i]=read();
    build();
    while(m--){
        int p=read(),b=read();
        update(p,p,b);
        cout<<tree[1]<<'\n';
    }
}
signed main() {
    hhhh();
    return 0;
}


```