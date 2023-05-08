---
title: 单调队列模板
description: 作者：open17
slug: MonotonicQueue
date: 2023-05-08 00:00:00+0000
categories:
    - DS
tags:
    - templates
    - c++
    - MonotonicQueue
    - luogu
---
## 模板
```cpp
    FOR(p,0,n){
        while(!maxs.empty()&&maxs.back()<a[p])maxs.pop_back();
        while(!mins.empty()&&mins.back()>a[p])mins.pop_back();
        maxs.push_back(a[p]);
        mins.push_back(a[p]);
        ans1[p]=maxs.front();
        ans2[p]=mins.front();
        if(p-k>=-1&&maxs.front()==a[p-k+1])maxs.pop_front();
        if(p-k>=-1&&mins.front()==a[p-k+1])mins.pop_front();
    }
```

# 滑动窗口 /【模板】单调队列

## 题目描述

有一个长为 $n$ 的序列 $a$，以及一个大小为 $k$ 的窗口。现在这个从左边开始向右滑动，每次滑动一个单位，求出每次滑动后窗口中的最大值和最小值。

例如：

The array is $[1,3,-1,-3,5,3,6,7]$, and $k = 3$。

![](https://cdn.luogu.com.cn/upload/pic/688.png)

## 输入格式

输入一共有两行，第一行有两个正整数 $n,k$。
第二行 $n$ 个整数，表示序列 $a$

## 输出格式

输出共两行，第一行为每次窗口滑动的最小值   
第二行为每次窗口滑动的最大值

## 样例 #1

### 样例输入 #1

```
8 3
1 3 -1 -3 5 3 6 7
```

### 样例输出 #1

```
-1 -3 -3 -3 3 3
3 3 5 5 6 7
```

## 提示

【数据范围】    
对于 $50\%$ 的数据，$1 \le n \le 10^5$；  
对于 $100\%$ 的数据，$1\le k \le n \le 10^6$，$a_i \in [-2^{31},2^{31})$。

## code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=1e6;
int a[N],ans1[N],ans2[N];
deque<int> maxs,mins;
int main() {
    ios
    int n,k;
    cin>>n>>k;
    FOR(i,0,n){
        cin>>a[i];
    }
    FOR(p,0,n){
        while(!maxs.empty()&&maxs.back()<a[p])maxs.pop_back();
        while(!mins.empty()&&mins.back()>a[p])mins.pop_back();
        maxs.push_back(a[p]);
        mins.push_back(a[p]);
        ans1[p]=maxs.front();
        ans2[p]=mins.front();
        if(p-k>=-1&&maxs.front()==a[p-k+1])maxs.pop_front();
        if(p-k>=-1&&mins.front()==a[p-k+1])mins.pop_front();
    }
    FOR(i,k-1,n){
        cout<<ans2[i]<<" ";
    }
    cout<<endl;
    FOR(i,k-1,n){
        cout<<ans1[i]<<" ";
    }
    cout<<endl;
    return 0;
}
```