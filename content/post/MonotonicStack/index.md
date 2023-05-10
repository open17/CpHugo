---
title: 单调栈模板
description: 通常用于解决NGE相关问题的一种数据结构
slug: MonotonicStack
date: 2023-05-08 00:00:00+0000
categories:
    - DS
tags:
    - templates
    - c++
    - NGE
    - luogu
    - MonotonicStack
---
## 模板1
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
## 模板2
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
# 【模板】单调栈

## 题目背景

模板题，无背景。  

2019.12.12 更新数据，放宽时限，现在不再卡常了。

## 题目描述

给出项数为 $n$ 的整数数列 $a_{1 \dots n}$。

定义函数 $f(i)$ 代表数列中第 $i$ 个元素之后第一个大于 $a_i$ 的元素的**下标**，即 $f(i)=\min_{i<j\leq n, a_j > a_i} \{j\}$。若不存在，则 $f(i)=0$。

试求出 $f(1\dots n)$。

## 输入格式

第一行一个正整数 $n$。

第二行 $n$ 个正整数 $a_{1\dots n}$。

## 输出格式

一行 $n$ 个整数 $f(1\dots n)$ 的值。

## 样例 #1

### 样例输入 #1

```
5
1 4 2 3 5
```

### 样例输出 #1

```
2 5 4 5 0
```

## 提示

【数据规模与约定】

对于 $30\%$ 的数据，$n\leq 100$；

对于 $60\%$ 的数据，$n\leq 5 \times 10^3$ ；

对于 $100\%$ 的数据，$1 \le n\leq 3\times 10^6$，$1\leq a_i\leq 10^9$。

## CODE1
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
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
int main() {
    ios
    int n;
    cin>>n;
    FOR(i,1,n+1)cin>>a[i];
    NGE(n);
    FOR(i,1,n+1)cout<<b[i]<<' ';
    return 0;
}
```
## CODE2
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=3e6+3;
int a[N],b[N];
void NGE(int n){
    stack<int> s;
    for(int i=n;i>0;i--){
        while(!s.empty()&&a[s.top()]<=a[i]){
            s.pop();
        }
        if(!s.empty()){
            b[i]=s.top();
        }
        s.push(i);
    }
}
int main() {
    ios
    int n;
    cin>>n;
    FOR(i,1,n+1)cin>>a[i];
    NGE(n);
    FOR(i,1,n+1)cout<<b[i]<<' ';
    return 0;
}
```