---
title: 对拍模板
description: 一种常见的技巧
slug: duipai
date: 2023-05-23 00:00:00+0000
tags:
    - skill
    - c++
---
## windows
### 对拍主程序
```cpp
#include<iostream>
#include<cstdio>
#include<cstdlib>
#include<ctime>
#include<windows.h>
int main(){
    int cnt=0;
    system("g++ 1.cpp -o 1.exe");
    system("g++ 2.cpp -o 2.exe");
    system("g++ data.cpp -o data.exe");
    while(1){
        cnt++;
        system("data.exe");
        printf("data create successfully\n");
        Sleep(1000);
        system("1.exe");
        system("2.exe");
        if(!system("fc res.out ans.out")){
            printf("AC test#%d\n",cnt);
        }
        else{
            printf("WA!\n");
            Sleep(2000);
            break;
        }
    }
    return 0;
}
```
### 数据生成
```cpp
#include<iostream>
#include<cstdio>
#include<cstdlib>
#include<ctime>
using namespace std;
typedef long long ll;
ll random(ll mod)
{
    ll n1, n2, n3, n4, ans;
    n1 = rand();
    n2 = rand();
    n3 = rand();
    n4 = rand();
    ans = n1 * n2 % mod;
    ans = ans * n3 % mod;
    ans = ans * n4 % mod;
    return ans;
}
int main(){
    freopen("data.in","w",stdout);
    srand((unsigned)time(0));
    ll i=random(10);
    cout<<i<<endl;
    return 0;
}
```
### 程序对拍节点
```cpp
//1.cpp
    freopen("data.in","r",stdin);
    freopen("res.out","w",stdout);
//2.cpp
    freopen("data.in","r",stdin);
    freopen("ans.out","w",stdout);
```

## linux
把exe改成out,fc改成diff,Sleep改成sleep,windows.h改为unistd.h