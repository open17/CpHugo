---
title: lc weekly contest 349 
description: 质量不错的一场
slug: lc-weekly-contest-349
date: 2023-06-03 00:00:00+0000
tags:
    - Leetcode
---
## 既不是最小值也不是最大值
### 题目
```    
给你一个整数数组 nums ，数组由 不同正整数 组成，请你找出并返回数组中 任一 既不是 最小值 也不是 最大值 的数字，如果不存在这样的数字，返回 -1 。
返回所选整数。
  示例 1：
输入：nums = [3,2,1,4]
输出：2
解释：在这个示例中，最小值是 1 ，最大值是 4 。因此，2 或 3 都是有效答案。
示例 2：
输入：nums = [1,2]
输出：-1
解释：由于不存在既不是最大值也不是最小值的数字，我们无法选出满足题目给定条件的数字。因此，不存在答案，返回 -1 。
示例 3：
输入：nums = [2,1,3]
输出：2
解释：2 既不是最小值，也不是最大值，这个示例只有这一个有效答案。 
  提示：
1 <= nums.length <= 100
1 <= nums[i] <= 100
nums 中的所有数字互不相同
```    
### 代码
模拟即可
```py
class Solution:
    def findNonMinOrMax(self, nums: List[int]) -> int:
        if len(nums)<=2:
            return -1
        nums.sort()
        return nums[1]
```
## 执行子串操作后的字典序最小字符串
### 题目
```    
给你一个仅由小写英文字母组成的字符串 s 。在一步操作中，你可以完成以下行为：
选则 s 的任一非空子字符串，可能是整个字符串，接着将字符串中的每一个字符替换为英文字母表中的前一个字符。例如，'b' 用 'a' 替换，'a' 用 'z' 替换。
返回执行上述操作 恰好一次 后可以获得的 字典序最小 的字符串。
子字符串 是字符串中的一个连续字符序列。
现有长度相同的两个字符串 x 和 字符串 y ，在满足 x[i] != y[i] 的第一个位置 i 上，如果  x[i] 在字母表中先于 y[i] 出现，则认为字符串 x 比字符串 y 字典序更小 。
  示例 1：
输入：s = "cbabc"
输出："baabc"
解释：我们选择从下标 0 开始、到下标 1 结束的子字符串执行操作。 
可以证明最终得到的字符串是字典序最小的。
示例 2：
输入：s = "acbbc"
输出："abaab"
解释：我们选择从下标 1 开始、到下标 4 结束的子字符串执行操作。
可以证明最终得到的字符串是字典序最小的。
示例 3：
输入：s = "leetcode"
输出："kddsbncd"
解释：我们选择整个字符串执行操作。
可以证明最终得到的字符串是字典序最小的。
  提示：
1 <= s.length <= 3 * 105
s 仅由小写英文字母组成
```    
### 代码
贪心+滑窗找到第一段非a的最大字段长度
注意特判全是a的情况
```py
class Solution:
    def smallestString(self, s: str) -> str:
        ans=""
        flag=1
        l=r=-1
        size=len(s)
        # 找第一段非a的最大字段长度
        for i in range(size):
            if flag and s[i]!='a':
                l=r=i
                # [l,r)
                while r<size and s[r]!='a':
                    r+=1
                flag=0
                break
        for i in range(size):
            if i==size-1 and s[i]=='a' and flag:
                ans+='z'
                break
            if l<=i<r:
                ans+=chr(ord(s[i])-1)
            else:
                ans+=s[i]
        return ans
```
## 收集巧克力
### 题目
```    
给你一个长度为 n 、下标从 0 开始的整数数组 nums ，表示收集不同巧克力的成本。每个巧克力都对应一个不同的类型，最初，位于下标 i 的巧克力就对应第 i 个类型。
在一步操作中，你可以用成本 x 执行下述行为：
同时对于所有下标 0 <= i < n - 1 进行以下操作， 将下标 i 处的巧克力的类型更改为下标 (i + 1) 处的巧克力对应的类型。如果 i == n - 1 ，则该巧克力的类型将会变更为下标 0 处巧克力对应的类型。
假设你可以执行任意次操作，请返回收集所有类型巧克力所需的最小成本。
  示例 1：
输入：nums = [20,1,15], x = 5
输出：13
解释：最开始，巧克力的类型分别是 [0,1,2] 。我们可以用成本 1 购买第 1 个类型的巧克力。
接着，我们用成本 5 执行一次操作，巧克力的类型变更为 [2,0,1] 。我们可以用成本 1 购买第 0 个类型的巧克力。
然后，我们用成本 5 执行一次操作，巧克力的类型变更为 [1,2,0] 。我们可以用成本 1 购买第 2 个类型的巧克力。
因此，收集所有类型的巧克力需要的总成本是 (1 + 5 + 1 + 5 + 1) = 13 。可以证明这是一种最优方案。
示例 2：
输入：nums = [1,2,3], x = 4
输出：6
解释：我们将会按最初的成本收集全部三个类型的巧克力，而不需执行任何操作。因此，收集所有类型的巧克力需要的总成本是 1 + 2 + 3 = 6 。
  提示：
1 <= nums.length <= 1000
1 <= nums[i] <= 109
1 <= x <= 109
```    
### 代码
> 涉及全部区间操作,考虑枚举每次操作   

看数据范围O(n2)做法即可     
找规律(见下)->枚举每次操作->转换为RMQ问题    
容易看出转移方程,用DP预处理RMQ即可(也可以ST表/压为O(n)空间DP)   

事实上这里RMQ预处理转化为NGE问题(单调栈)只需要O(n)时间复杂度[^1]

```py
class Solution:
    def minCost(self, nums: List[int], x: int) -> int:
        """
        顺序影响?
            Y
        规律:
            [a,b,c,d]  x
            
            [0,1,2,3]
            
            0: a x+b 2*x+c 3*x+d
            1: b x+c 2*x+d 3*x+a
            2: c x+d 2*x+a 3*x+b
            3: d x+a 2*x+b 3*x+c
        
        基础花费: 
        
                    sum(nums)
                    
        特殊花费(最高移动为cost):
        
                    cost=0  a+b+c+d
                    cost=1  min(a,b)+min(b,c)+min(c,d)+min(a,d) + x
                    cost=2  min(a,b,c)+min(b,c,d)+min(c,d,a)+min(d,a,b)+2*x
                    cost=3: min(a,b,c,d)*4+3*x
        """
        cost0=sum(nums)
        size=len(nums)
        dp=[[0]*size for _ in range(size)]
        for i in range(len(nums)):
            dp[0][i]=nums[i]
        ans=cost0
        for i in range(1,len(nums)):
            cnt=0
            for j in range(len(nums)):
                k=j+1 if j+1<len(nums) else 0
                dp[i][j]=min(dp[i-1][j],dp[i-1][k])
                cnt+=dp[i][j]
            ans=min(ans,cnt+i*x)
        return ans
```
## 最大和查询
### 题目
```    
给你两个长度为 n 、下标从 0 开始的整数数组 nums1 和 nums2 ，另给你一个下标从 1 开始的二维数组 queries ，其中 queries[i] = [xi, yi] 。
对于第 i 个查询，在所有满足 nums1[j] >= xi 且 nums2[j] >= yi 的下标 j (0 <= j < n) 中，找出 nums1[j] + nums2[j] 的 最大值 ，如果不存在满足条件的 j 则返回 -1 。
返回数组 answer ，其中 answer[i] 是第 i 个查询的答案。
  示例 1：
输入：nums1 = [4,3,1,2], nums2 = [2,4,9,5], queries = [[4,1],[1,3],[2,5]]
输出：[6,10,7]
解释：
对于第 1 个查询：xi = 4 且 yi = 1 ，可以选择下标 j = 0 ，此时 nums1[j] >= 4 且 nums2[j] >= 1 。nums1[j] + nums2[j] 等于 6 ，可以证明 6 是可以获得的最大值。
对于第 2 个查询：xi = 1 且 yi = 3 ，可以选择下标 j = 2 ，此时 nums1[j] >= 1 且 nums2[j] >= 3 。nums1[j] + nums2[j] 等于 10 ，可以证明 10 是可以获得的最大值。
对于第 3 个查询：xi = 2 且 yi = 5 ，可以选择下标 j = 3 ，此时 nums1[j] >= 2 且 nums2[j] >= 5 。nums1[j] + nums2[j] 等于 7 ，可以证明 7 是可以获得的最大值。
因此，我们返回 [6,10,7] 。
示例 2：
输入：nums1 = [3,2,5], nums2 = [2,3,4], queries = [[4,4],[3,2],[1,1]]
输出：[9,9,9]
解释：对于这个示例，我们可以选择下标 j = 2 ，该下标可以满足每个查询的限制。
示例 3：
输入：nums1 = [2,1], nums2 = [2,3], queries = [[3,3]]
输出：[-1]
解释：示例中的查询 xi = 3 且 yi = 3 。对于每个下标 j ，都只满足 nums1[j] < xi 或者 nums2[j] < yi 。因此，不存在答案。 
  提示：
nums1.length == nums2.length 
n == nums1.length 
1 <= n <= 105
1 <= nums1[i], nums2[i] <= 109 
1 <= queries.length <= 105
queries[i].length == 2
xi == queries[i][1]
yi == queries[i][2]
1 <= xi, yi <= 109
```    
### 代码
线段树维护(离散化/动态开点)
```cpp  
class Solution {
public:
    vector<int> maximumSumQueries(vector<int>& nums1, vector<int>& nums2, vector<vector<int>>& queries) {
    }
};
```



[^1]:源自何老师的题解