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