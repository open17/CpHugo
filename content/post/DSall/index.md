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
### 补充
技巧：事先压入一个边界元素到栈底，这样保证循环时栈一定不会为空，从而简化逻辑(源自0x3f)             
还要我发现我总结的上面的两个模板,灵神有个更本质的解释:https://leetcode.cn/problems/next-greater-node-in-linked-list/solution/tu-jie-dan-diao-zhan-liang-chong-fang-fa-v9ab/        
### 练习
#### 传统单调栈系列
```cpp
//https://leetcode.cn/problems/next-greater-element-i/
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        stack<int> a;
        map<int,int> m;
        vector<int> ans;
        for(int i=0;i<nums1.size();i++){
            m[nums1[i]]=i;
            ans.push_back(-1);
        }
        //max=1e4
        a.push(1e4+1);
        for(auto i:nums2){
            while(a.top()<i){
                int x=a.top();
                a.pop();
                if(m.count(x)){
                    ans[m[x]]=i;
                }
            }
            a.push(i);
        }
        return ans;
    }
};
//https://leetcode.cn/problems/next-greater-element-ii/
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        stack<int> a;
        int s=nums.size();
        vector<int> ans(s,-1);
        nums.push_back(1e9+1);
        a.push(s);
        for(int i=0;i<2*s-1;i++){
            while(nums[a.top()]<nums[i%s]){
                ans[a.top()]=nums[i%s];
                a.pop();
            }
            a.push(i%s);
        }
        return ans;
    }
};

```