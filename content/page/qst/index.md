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