---
title: 数据结构学习合集
description: 参考https://github.com/EndlessCheng/codeforces-go
slug: DSall
date: 2023-06-04 00:00:00+0000
categories:
    - DS
---
## 单调栈
### 模板1
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
### 模板2
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
### 练习
```cpp





```