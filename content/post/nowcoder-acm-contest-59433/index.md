---
slug: nowcoder-acm-contest-59433
title:  2023年国际大学生程序设计竞赛（ACM-ICPC）新疆赛区(重现赛)
description: 实力有限XD
date: 2023-05-01 00:00:00+0000
categories:
    - Others
tags:
    - ACM
---
## H 签到题
### 题目概述
如长度为7的字母三角形如下:
ABCDEFG  
HIJKLM   
NOPQR   
STUV  
WXY  
ZA  
B  
问长为n的字母三角形第a行第b个是什么字母?
### 输入
一行
`n a b `
### 输出
一个字符
### 例
- in: 4 2 3
- out: G

- in: 7 7 1
- out: B
### 思路
不难找出规律这个字母为`(n+n-1+..+(n-a+2)+b)%26`
```cpp
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
const int MOD=26;
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


inline void hhhh(){
    ll n,a,b;
    cin>>n>>a>>b;
    //ABCD EFG HI J
    //n+n-1+..+(n-a+2)  +b
    ll x=(n-a+2+n)*(a-1)/2;
    x%=MOD;
    x+=b%MOD;
    x%=MOD;
    cout<<char(x+'A'-1)<<'\n';
}

int main() {
    hhhh();
//     int T;
//     T.read();
//     while(T--){
//         hhhh();
//     }
    return 0;
}
```
## J 签到题
### 题目
Given a tree with n nodes numbered from 1 to n.
Alice wants to know the number of connected components with a size of three in the tree.
### 输入
第一行n节点数(1≤n≤$10^5$)        
n-1行每行两个节点表示u,v表示u,v连通(1<=u,v<=n)
### 输出
大小为3的连通子图的数量
### test
```
3
1 2
2 3
```
ans:`1`
```
5
1 2
1 3
1 4
2 5
```
ans:`4`
### 思路
错误1:没有估计好大小,实际上int不够   
错误2:以为u\<v,建图的时候没有考虑到        
找规律:
```cpp
/*
          1
          
    2     3     4 
                    
5     6            

层数>=3   都加上1

从第2层   C(n,2)

*/
```
bfs遍历一遍按照规律计算即可
### code
```cpp
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
ll n;
ll cb(ll n){
    if(n<2)return 0;
    if(n==2)return 1;
    return n*(n-1)/2;
}
vector<vector<ll>> G;
set<ll> visited;
inline void hhhh(){
    cin>>n;
    G.resize(n+3);
    ll u,v;
    For(i,1,n){
        cin>>u>>v;
        G[u].push_back(v);
        G[v].push_back(u);
    }
    queue<ll> q;
    q.push(1);
    visited.insert(1);
    ll depth=0;
    ll ans=0;
    while(!q.empty()){
        ll sizes=q.size();
        if(depth>=2){
            ans+=sizes;
        }
        For(i,0,sizes){
            ll node=q.front();
            q.pop();
            ll num=0;
            for(auto x:G[node]){
                if(visited.count(x))continue;
                num++;
                q.push(x);
                visited.insert(x);
            }
            ans+=cb(num);
        }
        depth++;
    }
    cout<<ans<<'\n';
}

int main() {
    hhhh();
    return 0;
}
```
## E签到题
### 题目
给你一个长为n的正数数组A,给出它的对应**正数**数组B   
B数组要满足以下条件:
- 元素不在A中
- 与A中对应(You can specify the correspondence relationship arbitrarily, but the relationship must be consistent and unique.For example, if you specify that the number 3 in the first line corresponds to the number 1 in the second line, then another non-3 number in the first line cannot correspond to the number 1, and all 3s in the first line must correspond to 1.)
### 输入
第一行n长度[1,$10^5$]    
第二行n个数字,[1,$10^9$]
### 输出
B数组,如有多个输出字典序最小的那个
### 样例
```
6
3 3 4 2 4 7
```
ans:`1 1 5 6 5 8`    
解释:  
Let 3 correspond to 1, 4 correspond to 5, 2 correspond to 6, and 7 correspond to 8, then the second line is [1, 1, 5, 6, 5, 8]. This is the smallest in lexicographic order. If we let 3 correspond to 9, the second line would be [9, 9, 5, 6, 5, 8], which is also a valid second line, but not the smallest one required by the problem.
### 思路
维护一个set去重A,然后再遍历一遍A并同时维护一个哈希表即可
### code
```cpp
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
const int N=1e5+4;
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

int a[N];
set<int> b;
map<int,int> ans;
inline void hhhh(){
    int n;
    n=read();
    For(i,0,n){
        a[i]=read();
        b.insert(a[i]);
    }
    int s=1;
    For(i,0,n){
        if(!ans.count(a[i])){
            while(b.count(s))s++;
            ans[a[i]]=s++;
        }
        cout<<ans[a[i]]<<' ';
    }
    //todo
}

int main() {
    hhhh();
//     int T;
//     T.read();
//     while(T--){
//         hhhh();
//     }
    return 0;
}
```