---
title: 小蓝书0X04二分法
description: 算法进阶指南0x04总结
slug: blue04
date: 2023-05-26 00:00:00+0000
categories:
    - Blue
tags:
    - Binary search
---
## 102. 最佳牛围栏

### 题目描述
农夫约翰的农场由 $N$ 块田地组成，每块地里都有一定数量的牛，其数量不会少于 1 头，也不会超过 2000 头。

约翰希望用围栏将一部分连续的田地围起来，并使得围起来的区域内每块地包含的牛的数量的平均值达到最大。

围起区域内至少需要包含 $F$ 块地，其中 $F$ 会在输入中给出。

在给定条件下，计算围起区域内每块地包含的牛的数量的平均值可能的最大值是多少。

### 输入格式
第一行输入整数 $N$ 和 $F$，数据间用空格隔开。

接下来 $N$ 行，每行输入一个整数，第 $i+1$ 行输入的整数代表第 $i$ 片区域内包含的牛的数目。

### 输出格式
输出一个整数，表示平均值的最大值乘以 1000 再向下取整之后得到的结果。

### 数据范围
$1≤N≤100000$

$1≤F≤N$

### 输入样例：
```
10 6
6 
4
2
10
3
8
5
9
4
1
```

### 输出样例：
```
6500
```
### tag
- 思维
- 二分
- DP/前缀和
### code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f3f3f3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=1e5+2;
double a[N],b[N];
int n,f;
bool check(double t){
    FOR(i,1,n+1){
        b[i]=a[i]+b[i-1]-t;
    }
    double mins=inf;
    double maxs=-inf;
    FOR(i,f,n+1){
        mins=min(mins,b[i-f]);
        maxs=max(maxs,b[i]-mins);
    }
    return maxs>=0;
}
int main() {
    ios
    cin>>n>>f;
    FOR(i,1,n+1){
        cin>>a[i];
    }
    double l=1,r=2001;
    double eps=1e-5;
    while(r-l>eps){
        double mid=(l+r)/2;
        if (check(mid))l=mid;
        else r=mid;
    }
    cout<<int(r*1000)<<'\n';
    return 0;
}
```
## 元素排序

有 $N$ 个元素，编号 $1,2,\dots,N$，每一对元素之间的大小关系是确定的，关系具有反对称性，但不具有传递性。元素的大小关系是 $N$ 个点与 $\frac{N\times(N-1)}{2}$ 条有向边构成的任意有向图。

然而，这是一道交互式试题，这些关系不能一次性得知，你必须通过不超过 $10000$ 次提问来获取信息，每次提问只能了解某两个元素之间的关系。

现在请你把这 $N$ 个元素排成一行，使得每个元素都小于右边与它相邻的元素。

你可以通过我们预设的 bool 函数 compare 来获得两个元素之间的大小关系。

例如，编号为 $a$ 和 $b$ 的两个元素，如果元素 $a$ 小于元素 $b$，则 compare(a,b) 返回 true，否则返回 false。

将 $N$ 个元素排好序后，把它们的编号以数组的形式输出，如果答案不唯一，则输出任意一个均可。

### 数据范围

$1 \leq N \leq 1000$

### 输入样例

```
[[0, 1, 0], [0, 0, 0], [1, 1, 0]]
```

### 输出样例

```
[3, 1, 2]
```
### code
```cpp
//满足归并排序性质，先水过去吧
// Forward declaration of compare API.
// bool compare(int a, int b);
// return bool means whether a is less than b.
class Solution {
public:
    vector<int> specialSort(int N) {
        vector<int>a;
        for(int i=1;i<=N;++i)a.push_back(i);
        stable_sort(a.begin(),a.end(),compare);
        return a;
    }
};
```