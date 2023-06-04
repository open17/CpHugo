---
title: "快捷"
slug: "qst"
menu:
    main: 
        weight: 2
        params:
            icon: clock
---
## 输入输出
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
## 常见套路
|key|算法|
|-----|-----|
|最大最小  |  二分/倍增|
|覆盖求整体 | 逆序|
|单纯的多次删除   |   链表模拟|
|中位数   |   对顶堆|
|第k大   |    堆/快选|
|逆序对    |    CDQ|
|维护传递关系  |  并查集|
|加法乘法取余| 分布取余|
|除法取余  |  逆元/逆序|
|NGE   |     单调栈|
| 维护滑动窗口的最值 |  单调队列|
| 区间操作转为单点操作|前缀和/差分|
|在数组找任意两个数满足...|考虑哈希表(如两数之和)|
|小于x的全部素数|欧拉筛|
|含有多次pow的大数程序优化|qpow|
|维护区间符合交换律的信息|线段树|
|绝对众数|摩尔投票|
|成环数组|暴力拼接/分三类(一般)讨论|
|n个数无限取,拼凑满足..|同余最短路|
|组合数对素数的模|卢卡斯定理|
|区间最值|ST|
|数位与计数|数位DP|
|范围大实际数量小|离散化|

