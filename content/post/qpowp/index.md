---
title: 快速幂取余模板
description: 作者：open17
slug: qpowp
date: 2023-05-05 00:00:00+0000
image: cover.jpg
categories:
    - Alg
tags:
    - templates
    - c++
    - qpow
    - luogu
---
## 模板
```cpp
ll qpow(ll a,ll b,ll p){
    ll ans=1%p;
    while(b){
        if(b&1)ans=(ans*a)%p;
        b>>=1;  
        a=(a*a)%p;
    }
    return ans;
}
```
## 题目描述

给你三个整数 $a,b,p$，求 $a^b \bmod p$。

## 输入格式

输入只有一行三个整数，分别代表 $a,b,p$。

## 输出格式

输出一行一个字符串 `a^b mod p=s`，其中 $a,b,p$ 分别为题目给定的值， $s$ 为运算结果。

## 样例 #1

### 样例输入 #1

```
2 10 9
```

### 样例输出 #1

```
2^10 mod 9=7
```

## 提示

**样例解释**

$2^{10} = 1024$，$1024 \bmod 9 = 7$。

**数据规模与约定**

对于 $100\%$ 的数据，保证 $0\le a,b < 2^{31}$，$a+b>0$，$2 \leq p \lt 2^{31}$。

## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
ll qpow(ll a,ll b,ll p){
    ll ans=1%p;
    while(b){
        if(b&1)ans=(ans*a)%p;
        b>>=1;  
        a=(a*a)%p;
    }
    return ans;
}
int main() {
    ios
    ll a,b,p;
    cin>>a>>b>>p;
    ll res=qpow(a,b,p);
    cout<<a<<"^"<<b<<" mod "<<p<<"="<<res<<endl;
    return 0;
}
```