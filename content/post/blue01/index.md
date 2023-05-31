---
title: 小蓝书0X01位运算
description: 算法进阶指南0x01总结
slug: blue01
date: 2023-04-26 00:00:00+0000
categories:
    - Blue
tags:
    - Bit
---
## a的b次方对p取模
### 前置知识
-  qpow 
-  math:$(a+b)%p=(a%p+b%p)%p$
### code
```cpp
// 求 a的 b次方对 p取模的值。

// 输入格式
// 三个整数 a,b,p，在同一行用空格隔开。

// 输出格式
// 输出一个整数，表示a^b mod p的值。

// 数据范围
// 0≤a,b≤10^9

// 1≤p≤109
// 输入样例：
// 3 2 7
// 输出样例：
// 2
#include <iostream>
using namespace std;
typedef long long ll;
int main(){
    ll a,b,p,res;
    cin>>a>>b>>p;
    // 防止当b=0，p=1时被卡
    res=1%p;
    while(b){
        if(b&1)res=(res*a)%p;
        a*=a;
        a%=p;
        b>>=1;
    }
    cout<<res<<endl;
    return 0;
}

```
## a*b对p取模
### 前置知识
-   qpow
-   math:`(a+b)%p=(a%p+b%p)%p `
### code
```cpp
// 求 a
//  乘 b
//  对 p
//  取模的值。

// 输入格式
// 第一行输入整数a
// ，第二行输入整数b
// ，第三行输入整数p
// 。

// 输出格式
// 输出一个整数，表示a*b mod p的值。

// 数据范围
// 1≤a,b,p≤1018
// 输入样例：
// 3
// 4
// 5
// 输出样例：
// 2
#include <iostream>
using namespace std;
typedef long long ll;
int main(){
    ll a,b,p,res=0;
    cin>>a>>b>>p;
    while(b){
        if(b&1)res=(res+a)%p;
        b>>=1;
        a*=2;
        a%=p;
    }
    cout<<res<<endl;
    return 0;
}
```
## 最短Hamilton路径
前置知识
-  旅行商问题:NP完全,没有多项式时间解法 
-  位运算 
-  状压DP 
-  bitset:STL 
```cpp
// 给定一张 n个点的带权无向图，点从 0∼n−1标号，求起点 0到终点 n−1的最短 Hamilton 路径。

// Hamilton 路径的定义是从 0到 n−1不重不漏地经过每个点恰好一次。输入格式
// 第一行输入整数 n。
// 接下来 n行每行 n个整数，其中第 i行第 j个整数表示点 i到 j的距离（记为 a[i,j]）。
// 对于任意的 x,y,z，数据保证 a[x,x]=0，a[x,y]=a[y,x]并且 a[x,y]+a[y,z]≥a[x,z]。

// 输出格式
// 输出一个整数，表示最短 Hamilton 路径的长度。

// 数据范围
// 1≤n≤20

// 0≤a[i,j]≤107
// 输入样例：
// 5
// 0 2 4 5 1
// 2 0 6 5 3
// 4 6 0 8 3
// 5 5 8 0 5
// 1 3 3 5 0
// 输出样例：
// 18
#include<iostream>
#include<algorithm>
#include<cstring>
using namespace std;
#define For(a,b,c) for(int a=b;a<c;a++)
#define inf 0x3f
const int N=20,M=1<<20;
int n;
//大数组开到全局里，防止爆栈
//f[i][j]: i:经过状态，j:j点最短路
int f[M][N],w[N][N];
int main(){
    cin>>n;
    For(i,0,n){
        For(j,0,n){
            cin>>w[i][j];
        }
    }
    memset(f,inf,sizeof(f));
    f[1][0]=0;
    For(i,0,1<<n){
        For(j,0,n){
            if(i>>j&1){
                //int p=i^(1<<j)
                int p=i-(1<<j);
                For(k,0,n){
                    if(p&(1<<k))
                    // if(p>>k&1)
                        f[i][j]=min(f[i][j],f[p][k]+w[k][j]);
                    
                }
            }
        }
    }
    cout<<f[(1<<n)-1][n-1]<<endl;
    return 0;
}
```
## 起床困难综合症
### 前置知识
-  位运算性质 :与或非运算在二进制表示下不进位，也就是说每个bit之间**独立**位运算
-  贪心
### 题目描述
21世纪，许多人得了一种奇怪的病：起床困难综合症，其临床表现为：起床难，起床后精神不佳。作为一名青春阳光好少年，atm 一直坚持与起床困难综合症作斗争。通过研究相关文献，他找到了该病的发病原因： 在深邃的太平洋海底中，出现了一条名为 drd 的巨龙，它掌握着睡眠之精髓，能随意延长大家的睡眠时间。
正是由于 drd 的活动，起床困难综合症愈演愈烈， 以惊人的速度在世界上传播。
为了彻底消灭这种病，atm 决定前往海底，消灭这条恶龙。
历经千辛万苦，atm 终于来到了 drd 所在的地方，准备与其展开艰苦卓绝的战斗。
drd 有着十分特殊的技能，他的防御战线能够使用一定的运算来改变他受到的伤害。   

具体说来，drd 的防御战线由 n扇防御门组成。
每扇防御门包括一个运算 op和一个参数 t ，其中运算一定是 OR,XOR,AND中的一种，参数则一定为非负整数。

如果还未通过防御门时攻击力为 x
则其通过这扇防御门后攻击力将变为 x op t

最终 drd 受到的伤害为对方初始攻击力 x
 依次经过所有 n扇防御门后转变得到的攻击力。

由于 atm 水平有限，他的初始攻击力只能为 0
 到 m之间的一个整数（即他的初始攻击力只能在 0,1,…,m中任选，
但在通过防御门之后的攻击力不受 m的限制）。

为了节省体力，他希望通过选择合适的初始攻击力使得他的攻击能让 drd 受到最大的伤害，请你帮他计算一下，他的一次攻击最多能使 drd 受到多少伤害。

### 输入格式
第 1行包含 2个整数，依次为 n,m，表示 drd 有 n扇防御门，atm 的初始攻击力为 0到 m之间的整数。

接下来 n  行，依次表示每一扇防御门。每行包括一个字符串 op  和一个非负整数 t ，两者由一个空格隔开，且 op  在前，t  在后，op  表示该防御门所对应的操作，t  表示对应的参数。

输出格式
输出一个整数，表示 atm 的一次攻击最多使 drd 受到多少伤害。

### 数据范围
![pic](https://cdn.acwing.com/media/article/image/2019/09/07/19_9f80784cd1-QQ%E6%88%AA%E5%9B%BE20190907125839.png)

### 输入样例：
3 10  
AND 5  
OR 6  
XOR 7  
输出样例：
1
### 样例解释
atm可以选择的初始攻击力为 0,1,…,10

假设初始攻击力为 4，最终攻击力经过了如下计算

4 AND 5 = 4

4 OR 6 = 6
6 XOR 7 = 1 
类似的，我们可以计算出初始攻击力为 1,3,5,7,9  时最终攻击力为 0 ，初始攻击力为 0,2,4,6,8,10  时最终攻击力为 1 ，因此 atm 的一次攻击最多使 drd 受到的伤害值为 1 
### code
```cpp
#include<iostream>
#include<vector>
#include<string>
#include<algorithm>
using namespace std;
#define For(a,b,c) for(int a=b;a<c;a++)
const int N=1e6;
vector<pair<string,int>> a(N);
string op;
int t;
int n,m;
#define ios ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
int change(int p,int q){
    For(i,0,n){
        int x=a[i].second>>p&1;
        if(a[i].first=="AND")q&=x;
        else if(a[i].first=="OR")q|=x;
        else {q^=x;}
    }
    return  q;
}
int main(){
    ios
    cin>>n>>m;
    For(i,0,n){
        cin>>a[i].first;
        cin>>a[i].second;
    }
    int pre=0,aft=0;
    For(i,0,30){
        int p=29-i;
        int pos1=change(p,0);
        int pos2=change(p,1);
        if(pre+(1<<p)<=m && pos2>pos1){
            pre+=1<<p;
            aft+=pos2<<p;
        }
        else aft+=pos1<<p;
    }
    cout<<aft<<endl;
}
```
## XOR成对变换
```py
if n&1:
    n^1==n-1
else:
    n^1==n+1
```
## lowbit
`n&(-n)`