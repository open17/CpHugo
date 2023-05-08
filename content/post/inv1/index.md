---
title: 乘法逆元模板
description: 基于扩展欧几里得算法的模板
slug: inv1
date: 2023-05-08 00:00:00+0000
categories:
    - Math
tags:
    - templates
    - c++
    - inv
---
## 模板
```cpp
long long extgcd(long long a, long long b, long long &x, long long &y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    long long d = extgcd(b, a % b, y, x);
    y -= a / b * x;
    return d;
}
long long inv(long long a, long long m) {
    long long x, y;
    if (extgcd(a, m, x, y) != 1) {
        return -1; // 不存在乘法逆元
    }
    return (x % m + m) % m;
}
```
