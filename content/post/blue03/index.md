---
title: 小蓝书0X03前缀和与差分
description: 算法进阶指南0x03总结
slug: blue03
date: 2023-04-26 00:00:00+0000
categories:
    - Blue
tags:
    - summary
    - c++
    - preSum
---
## 激光炸弹
### 题目
地图上有 $N$ 个目标，用整数 $X_i,Y_i$ 表示目标在地图上的位置，每个目标都有一个价值 $W_i$。

注意：不同目标可能在同一位置。

现在有一种新型的激光炸弹，可以摧毁一个包含 $R \times R$ 个位置的正方形内的所有目标。

激光炸弹的投放是通过卫星定位的，但其有一个缺点，就是其爆炸范围，即那个正方形的边必须和 $x,y$ 轴平行。

求一颗炸弹最多能炸掉地图上总价值为多少的目标。

**输入格式**  
第一行输入正整数 $N$ 和 $R$，分别代表地图上的目标数目和正方形包含的横纵位置数量，数据用空格隔开。

接下来 $N$ 行，每行输入一组数据，每组数据包括三个整数 $X_i,Y_i,W_i$，分别代表目标的 $x$ 坐标，$y$ 坐标和价值，数据用空格隔开。

**输出格式**  
输出一个正整数，代表一颗炸弹最多能炸掉地图上目标的总价值数目。

数据范围   
$0 \le R \le 10^9$

$0 < N \le 10^4, 0 \le X_i, Y_i \le 5000, 0 \le W_i \le 1000$

输入样例：   
2 1  
0 0 1  
1 1 1  
输出样例：  
1
### code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=5000+3;
int b[N][N];
int main() {
    ios
    int r,x,y,w,t;
    cin>>t>>r;
    while(t--){
        cin>>x>>y>>w;
        //标准开大一格
        b[x+1][y+1]+=w;
    }
    FOR(i,1,N)
        FOR(j,1,N)
            //题目卡内存，只能开一个数组，原地修改
            b[i][j]=b[i-1][j]+b[i][j-1]-b[i-1][j-1]+b[i][j];
    int ans=0;
    // 注意细节
    r=min(N-1,r);
    FOR(i,r,N){
        FOR(j,r,N){
            ans=max(b[i][j]-b[i-r][j]-b[i][j-r]+b[i-r][j-r],ans);
        }
    }
    cout << ans << endl;
    return 0;
}
```
## IncDec序列
> 很多时候，我们将区间操作转换为差分序列的单点操作，以降低难度
### 题目描述

给定一个长度为 $n$ 的数列 $a_1,a_2,\dots,a_n$，每次可以选择一个区间 $[l,r]$，使下标在这个区间内的数都加一或者都减一。

求至少需要多少次操作才能使数列中的所有数都一样，并求出在保证最少次数的前提下，最终得到的数列可能有多少种。

输入格式

第一行输入正整数 $n$。

接下来 $n$ 行，每行输入一个整数，第 $i+1$ 行的整数代表 $a_i$。

输出格式

第一行输出最少操作次数。

第二行输出最终能得到多少种结果。

数据范围

$0<n\le 10^5$,
$0\le a_i<2^{31}$

输入样例：  
4  
1  
1  
2  
2  

输出样例：  
1  
2  
### tag
- 思维
- 贪心
### code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=1e5+3;
ll a[N];
int main() {
    ios
    int n;
    cin>>n;
    FOR(i,1,n+1){
        cin>>a[i];
    }
    // 注意这里倒着
    for(int i=n;i>0;i--)a[i]-=a[i-1];
    ll cnt=0,cnt2=0;
    FOR(i,2,n+1){
        if(a[i]>0)cnt+=a[i];
        else cnt2-=a[i];
    }
    cout<<max(cnt,cnt2)<<'\n';
    cout<<abs(cnt2-cnt)+1<<'\n';
    return 0;
}
```
## 最高的牛
### 题目
有 N 头牛站成一行，被编队为 1、2、3…N，每头牛的身高都为整数。

当且仅当两头牛中间的牛身高都比它们矮时，两头牛方可看到对方。

现在，我们只知道其中最高的牛是第 P 头，它的身高是 H，剩余牛的身高未知。

但是，我们还知道这群牛之中存在着 M 对关系，每对关系都指明了某两头牛 A 和 B 可以相互看见。

求每头牛的身高的最大可能值是多少。

输入格式

第一行输入整数 N,P,H,M，数据用空格隔开。

接下来 M 行，每行输出两个整数 A 和 B，代表牛 A 和牛 B 可以相互看见，数据用空格隔开。

输出格式

一共输出 N 行数据，每行输出一个整数。

第 i 行输出的整数代表第 i 头牛可能的最大身高。

数据范围

$1≤N≤5000$，$1≤H≤1000000$，$1≤A,B≤10000$，$0≤M≤10000$

输入样例：

```py
9 3 5 5
1 3
5 3
4 3
3 7
9 8
```

输出样例：

```py
5
4
5
3
4
4
5
5
5
```

注意：此题中给出的关系对可能存在重复。
### code
```cpp
#include<bits/stdc++.h>
using namespace std;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define inf 0x3f
typedef long long ll;
typedef pair<int, int> pii;
const int N=5000+3;
set<pii> used;
int d[N];
int main() {
    ios
    int n,p,h,m,a,b;
    cin>>n>>p>>h>>m;
    while(m--){
        cin>>a>>b;
        if(a>b)swap(a,b);
        if(used.count(make_pair(a,b)))continue;
        d[a+1]--;
        d[b]++;
        used.insert(make_pair(a,b));
    }
    d[0]=h;
    FOR(i,1,n+1){
        d[i]+=d[i-1];
        cout<<d[i]<<'\n';
    }
    return 0;
}
```