---
title: 乘法逆元递推模板
description: 基于费马小定理快速求出多个连续的逆元
slug: inv2
date: 2023-05-08 00:00:00+0000
categories:
    - Math
tags:
    - templates
    - c++
    - inv
    - luogu
---
## 模板
- 只适用于模数为质数的情况(费马小定理)
```cpp
vector<long long> inv_vec(long long n, long long m) {
    vector<long long> inv(n + 1, 1);
    for (long long i = 2; i <= n; i++) {
        inv[i] = (m - m / i) * inv[m % i] % m;
    }
    return inv;
}
```
# 【模板】乘法逆元

## 题目背景

这是一道模板题

## 题目描述

给定 $n,p$ 求 $1\sim n$ 中所有整数在模 $p$ 意义下的乘法逆元。

这里 $a$ 模 $p$ 的乘法逆元定义为 $ax\equiv1\pmod p$ 的解。

## 输入格式

一行两个正整数 $n,p$。

## 输出格式

输出 $n$ 行，第 $i$ 行表示 $i$ 在模 $p$ 下的乘法逆元。

## 样例 #1

### 样例输入 #1

```
10 13
```

### 样例输出 #1

```
1
7
9
10
8
11
2
5
3
4
```

## 提示

$ 1 \leq n \leq 3 \times 10 ^ 6, n < p < 20000528 $

输入保证 $ p $ 为质数。
## code
```cpp
#include<iostream>
using namespace std;
const int N=3e6+2;
long long inv[N];
void inv_vec(long long n, long long m) {
    inv[0]=1;
    inv[1]=1;
    for (long long i = 2; i <= n; i++) {
        inv[i] = (m - m / i) * inv[m % i] % m;
        printf("%lld\n",inv[i]);
    }
}
int main(){
    int n,p;
    scanf("%d %d",&n,&p);
    printf("1\n");
    inv_vec(n,p);
    return 0;
}
```