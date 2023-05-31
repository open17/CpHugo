---
title: 算法输入输出模板
description: 一切的开始......
slug: template
date: 2023-05-08 00:03:00+0000
image: cover.jpg
categories:
    - Learn
tags:
    - Templates
---
## c++
### 精简模板
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


inline void hhhh(){
    //todo
}

int main() {
    //hhhh();
    int T;
    T.read();
    while(T--){
        hhhh();
    }
    return 0;
}
```
### 其它模板(来源网络)
```cpp
#define _USE_MATH_DEFINES
// C
#include <cassert>
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <cctype>
#include <cmath>           
#include <ctime>


//io
#include <iostream>        //基本输入输出流
#include <iomanip>
#include <sstream>         //基于字符串的流

//标准异常类
#include <stdexcept>       

//algorithm
#include <algorithm>       
#include <numeric>
#include <functional>      //定义运算函数（代替运算符）
#include <complex>         //复数类
#include <random>


//STL
#include <string>          //字符串类
#include <list>           //线性列表容器
#include <vector>          //动态数组容器
#include <stack>           //堆栈容器
#include <queue>           //队列容器
#include <deque>           //双端队列容器
#include <bitset>          //比特集合
#include <set>             //集合容器
#include <map>            //映射容器
#include <unordered_set>
#include <unordered_map>


using namespace std;

//fast ios
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);

#define ALL(a) (a).begin(),(a).end()
#define FOR(w, a, n) for(int w=(a);w<(n);++w)
#define RFOR(w, a, n) for(int w=(n)-1;w>=(a);--w)
#define REP(w, n) for(int w=0;w<int(n);++w)
#define RREP(w, n) for(int w=int(n)-1;w>=0;--w)
#define IN(a, x, b) (a<=x && x<b)
#define trace(...) __f(#__VA_ARGS__, __VA_ARGS__)


template <typename Arg1>
void __f(const char* name, Arg1&& arg1){
  cerr << name << ": " << arg1 << endl;
}
template <typename Arg1, typename... Args>
void __f(const char* names, Arg1&& arg1, Args&&... args){
  const char* comma = strchr(names + 1, ',');
  cerr.write(names, comma - names) << ": " << arg1 << " |";
  __f(comma + 1, args...);
}

typedef long long ll;
typedef pair<int, int> pii;
const double PI = acos(-1.0);
const double eps = 1e-6;
const int INF = 1 << 29;
const int MOD = 1e9 + 7;
const int MAXN = 100;

int main() {
    cout << "Hello, ACM." << endl;
    return 0;
}
```
## python
```py
import sys
import heapq
import random
from math import ceil,floor,fmod,gcd,sqrt,inf
from bisect import bisect_left
from collections import defaultdict,Counter,deque,OrderedDict
from functools import lru_cache,cmp_to_key

#sys.setrecursionlimit(1000000)

# 输入1
def ii():
    return int(sys.stdin.readline().strip())

# 输入2
def iin():
    return map(int,sys.stdin.readline().split())

def inn():
    return sys.stdin.readline().strip()
```
## java
## go