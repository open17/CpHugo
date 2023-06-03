---
title: lc weekly contest 302
description: 本场竞赛由「千挂科技 & 力扣」联合主办
slug: lc-weekly-contest-302
date: 2023-06-01 00:00:00+0000
tags:
    - Leetcode
image: https://pic.lingkou.xyz/1657181817-GjoGBU-1760-360%20%E5%8D%83%E6%8C%82%E7%A7%91%E6%8A%80.png
---
## 写在前面
***
## T1 数组能形成多少数对 
```
给你一个下标从 0 开始的整数数组 nums 。在一步操作中，你可以执行以下步骤：

从 nums 选出 两个 相等的 整数
从 nums 中移除这两个整数，形成一个 数对
请你在 nums 上多次执行此操作直到无法继续执行。

返回一个下标从 0 开始、长度为 2 的整数数组 answer 作为答案，其中 answer[0] 是形成的数对数目，answer[1] 是对 nums 尽可能执行上述操作后剩下的整数数目。

 

示例 1：

输入：nums = [1,3,2,1,3,2,2]
输出：[3,1]
解释：
nums[0] 和 nums[3] 形成一个数对，并从 nums 中移除，nums = [3,2,3,2,2] 。
nums[0] 和 nums[2] 形成一个数对，并从 nums 中移除，nums = [2,2,2] 。
nums[0] 和 nums[1] 形成一个数对，并从 nums 中移除，nums = [2] 。
无法形成更多数对。总共形成 3 个数对，nums 中剩下 1 个数字。
示例 2：

输入：nums = [1,1]
输出：[1,0]
解释：nums[0] 和 nums[1] 形成一个数对，并从 nums 中移除，nums = [] 。
无法形成更多数对。总共形成 1 个数对，nums 中剩下 0 个数字。
示例 3：

输入：nums = [0]
输出：[0,1]
解释：无法形成数对，nums 中剩下 1 个数字。
 

提示：

1 <= nums.length <= 100
0 <= nums[i] <= 100
```
### 思路
哈希记录数量再按照题目模拟(这里为了快用了py的Counter)
```py
class Solution:
    def numberOfPairs(self, nums: List[int]) -> List[int]:
        x=Counter(nums)
        print(x)
        cnt=0
        p=0
        for i in x.keys():
            if x[i]&1:
                cnt+=x[i]%2
            p+=x[i]//2
        return [p,cnt]
```
## T2 数位和相等数对的最大和 
```
给你一个下标从 0 开始的数组 nums ，数组中的元素都是 正 整数。请你选出两个下标 i 和 j（i != j），且 nums[i] 的数位和 与  nums[j] 的数位和相等。

请你找出所有满足条件的下标 i 和 j ，找出并返回 nums[i] + nums[j] 可以得到的 最大值 。

 

示例 1：

输入：nums = [18,43,36,13,7]
输出：54
解释：满足条件的数对 (i, j) 为：
- (0, 2) ，两个数字的数位和都是 9 ，相加得到 18 + 36 = 54 。
- (1, 4) ，两个数字的数位和都是 7 ，相加得到 43 + 7 = 50 。
所以可以获得的最大和是 54 。
示例 2：

输入：nums = [10,12,19,14]
输出：-1
解释：不存在满足条件的数对，返回 -1 。
 

提示：

1 <= nums.length <= 105
1 <= nums[i] <= 109
```
### 思路
类同leetcode第一题两数之和            
哈希条件改一下即可
```cpp
class Solution {
public:
    int getS(int n){
        int ans=0;
        while(n){
           ans+=n%10;
           n/=10;
        }
        return ans;
    }
    int maximumSum(vector<int>& nums) {
        map<int,int> mm;
        int res=-1;
        for(auto i:nums){
            int p=getS(i);
            if(mm.count(p)){
                res=max(res,mm[p]+i);
                mm[p]=max(mm[p],i);
            }
            else{
                mm.insert(make_pair(p,i));
            }
        }
        return res;
    }
};
```
## T4使数组可以被整除的最少删除次数
```
给你两个正整数数组 nums 和 numsDivide 。你可以从 nums 中删除任意数目的元素。

请你返回使 nums 中 最小 元素可以整除 numsDivide 中所有元素的 最少 删除次数。如果无法得到这样的元素，返回 -1 。

如果 y % x == 0 ，那么我们说整数 x 整除 y 。

 

示例 1：

输入：nums = [2,3,2,4,3], numsDivide = [9,6,9,3,15]
输出：2
解释：
[2,3,2,4,3] 中最小元素是 2 ，它无法整除 numsDivide 中所有元素。
我们从 nums 中删除 2 个大小为 2 的元素，得到 nums = [3,4,3] 。
[3,4,3] 中最小元素为 3 ，它可以整除 numsDivide 中所有元素。
可以证明 2 是最少删除次数。
示例 2：

输入：nums = [4,3,6], numsDivide = [8,2,6,10]
输出：-1
解释：
我们想 nums 中的最小元素可以整除 numsDivide 中的所有元素。
没有任何办法可以达到这一目的。
 

提示：

1 <= nums.length, numsDivide.length <= 105
1 <= nums[i], numsDivide[i] <= 109
```
### 思路
数学,先求出gcd,然后遍历一遍数组看看有没有gcd的因数即可
```py
class Solution:
    def minOperations(self, nums: List[int], numsDivide: List[int]) -> int:
        nums.sort()
        x=numsDivide[0]
        for i in numsDivide:
            x=gcd(x,i)
        # print(x)
        p=0
        while p<=len(nums):
            if p==len(nums):
                p=-1
                break
            if x%nums[p]==0:
                break
            p+=1
        return p
```