---
title: 欧拉筛模板
description: 作者：open17
slug: EulerSieve
date: 2023-05-08 00:00:00+0000
categories:
    - Math
tags:
    - templates
    - c++
    - EulerSieve
    - luogu
---
## 欧拉筛
```cpp
const int N=100;
int primes[N], cnt;
bool st[N];
void get_primes(int n)
{
    for (int i = 2; i <= n; i ++ )
    {
        if (!st[i]) primes[cnt ++ ] = i;
        for (int j = 0; primes[j] <= n / i; j ++ )
        {
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;
        }
    }
}
```
# 【模板】线性筛素数

## 题目背景

本题已更新，从判断素数改为了查询第 $k$ 小的素数  
提示：如果你使用  `cin` 来读入，建议使用 `std::ios::sync_with_stdio(0)` 来加速。

## 题目描述

如题，给定一个范围 $n$，有 $q$ 个询问，每次输出第 $k$ 小的素数。

## 输入格式

第一行包含两个正整数 $n,q$，分别表示查询的范围和查询的个数。

接下来 $q$ 行每行一个正整数 $k$，表示查询第 $k$ 小的素数。

## 输出格式

输出 $q$ 行，每行一个正整数表示答案。

## 样例 #1

### 样例输入 #1

```
100 5
1
2
3
4
5
```

### 样例输出 #1

```
2
3
5
7
11
```

## 提示

【数据范围】  
对于 $100\%$ 的数据，$n = 10^8$，$1 \le q \le 10^6$，保证查询的素数不大于 $n$。

Data by NaCly\_Fish.
## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=1e8;
int primes[N], cnt;
bool st[N];
void get_primes(int n)
{
    for (int i = 2; i <= n; i ++ )
    {
        if (!st[i]) primes[cnt ++ ] = i;
        for (int j = 0; primes[j] <= n / i; j ++ )
        {
            st[primes[j] * i] = true;
            if (i % primes[j] == 0) break;
        }
    }
}
int main() {
    ios
    int n,q;
    cin>>n>>q;
    get_primes(n);
    while(q--){
        int x;
        cin>>x;
        cout<<primes[x-1]<<endl;
    }
    return 0;
}
```