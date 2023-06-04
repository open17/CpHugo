---
title: 小蓝书0X06倍增---天才ACM
description: 算法进阶指南0x06总结
slug: blue06
date: 2023-05-27 01:00:00+0000
categories:
    - Blue
    - Alg
tags:
    - Binary Lifting
---

## 天才ACM
### 题目描述

给定一个整数 M，对于任意一个整数集合 S，定义“校验值”如下:

从集合 S 中取出 M 对数(即 2×M 个数，不能重复使用集合中的数，如果 S 中的整数不够 M 对，则取到不能取为止)，使得“每对数的差的平方”之和最大，这个最大值就称为集合 S 的“校验值”。

现在给定一个长度为 N 的数列 A 以及一个整数 T。

我们要把 A 分成若干段，使得每一段的“校验值”都不超过 T。

求最少需要分成几段。

### 样例

输入样例：  
2  
5 1 49  
8 2 1 7 9  
5 1 64  
8 2 1 7 9  
输出样例：  
2  
1  
### code
```cpp
#include <iostream>
#include <algorithm>
#include<cstdio>
#include<cstdlib>
#include<ctime>
using namespace std;
typedef long long ll;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
#define FOR(w, a, n) for(ll w=(a);w<(n);++w)
#define debug(a,b,c) cout<<'\n'<<"debug start"<<'\n';for(int i=a;i<=b;i++){cout<<c[i]<<' ';}cout<<'\n'<<"debug over"<<'\n'<<'\n';
#define inf 0x3f
typedef pair<int, int> pii;
const int N=5e6+9;
ll a[N],b[N],temp[N];
ll t;
ll k,m,n;
inline ll read() {
    ll x = 0, f = 1;
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
bool check(ll l,ll last,ll r){
    if(l==last){
        ll x=a[l];
        ll y=a[r];
        temp[l]=min(x,y);
        temp[r]=max(x,y);
        ll ans=(x-y)*(x-y);
        return ans<=t;
    }
    FOR(i,last+1,r+1){
        b[i]=a[i];
    }
    sort(b+last+1,b+r+1);
    //merge
    int p1=l,p2=last+1,pp=l;
    while(p1<=last&&p2<=r){
        if(b[p1]<b[p2])temp[pp++]=b[p1++];
        else temp[pp++]=b[p2++];
    }
    while(p1<=last)temp[pp++]=b[p1++];
    while(p2<=r)temp[pp++]=b[p2++];
    //check
    ll num=m;
    ll sums=0;
    ll ll=l,rr=r;
    while(num&&l<r){
        num--;
        sums+=(temp[r]-temp[l])*(temp[r]-temp[l]);
        l++;
        r--;
    }
    //cout<<"  l:"<<ll<<"  last:"<<last<<"  r:"<<rr<<"  sums:"<<sums<<'\n';
    //debug(ll,rr,temp)
    return sums<=t;
}
int main() {
    // freopen("data.in","r",stdin);
    // freopen("ans.out","w",stdout);
    k=read();
    while(k--){
        n=read();
        m=read();
        t=read();
        FOR(i,1,n+1)a[i]=read();
        //strat from 1 ,[l,r+size]
        ll cnt=0,l=1,r=1,size=1;
        while(r<n+1){
            while(size){
                if(r+size<n+1&&check(l,r,r+size)){
                    r+=size;
                    size*=2;
                    FOR(i,l,r+1)b[i]=temp[i];
                    //cout<<"ss"<<endl;
                    //debug(l,r,b)
                    //cout<<"ss"<<endl;
                }
                else{
                    size/=2;
                }
            }
            //cout<<"!!!!!!!!!!!"<<r<<" "<<l<<'\n';
            cnt++;
            size=1;
            r++;
            l=r;
        }
        cout << cnt << endl;
    }
    return 0;
}
```
## st表
详见st表模板