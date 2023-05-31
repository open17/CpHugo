---
title: lc weekly contest 313
description: 本场竞赛由「 Airwallex 空中云汇 & 力扣」联合主办
slug: lc-weekly-contest-313 
date: 2023-05-26 00:00:00+0000
tags:
    - Leetcode
image: https://pic.lingkou.xyz/1664008640-fTlCRH-1760-360%20%E7%A9%BA%E4%B8%AD%E4%BA%91%E6%B1%87.png   
---
> 痛苦T4
## T1 公因子的数目
给你两个正整数 a 和 b ，返回 a 和 b 的 公 因子的数目。

如果 x 可以同时整除 a 和 b ，则认为 x 是 a 和 b 的一个 公因子 。


示例 1：

输入：a = 12, b = 6
输出：4
解释：12 和 6 的公因子是 1、2、3、6 。
示例 2：

输入：a = 25, b = 30
输出：2
解释：25 和 30 的公因子是 1、5 。
 

提示：

1 <= a, b <= 1000
### 思路
模拟即可
```cpp
class Solution {
public:
    int commonFactors(int a, int b) {
        int t=min(a,b);
        int cnt=0;
        for(int i=1;i<=t;i++){
            if(a%i==0&&b%i==0)cnt++;
        }
        return cnt;
    }
};
```
## T2 沙漏的最大总和
给你一个大小为 m x n 的整数矩阵 grid 。   

按以下形式将矩阵的一部分定义为一个 沙漏 ：   
![沙漏图片](https://assets.leetcode.com/uploads/2022/08/21/img.jpg)
返回沙漏中元素的 最大 总和。   

注意：沙漏无法旋转且必须整个包含在矩阵中。   

 

示例 1：   
![](https://assets.leetcode.com/uploads/2022/08/21/1.jpg)  

输入：grid = [[6,2,1,3],[4,2,1,5],[9,2,8,7],[4,1,2,9]\]   
输出：30   
解释：上图中的单元格表示元素总和最大的沙漏：6 + 2 + 1 + 2 + 9 + 2 + 8 = 30 。   
示例 2：
![](https://assets.leetcode.com/uploads/2022/08/21/2.jpg)

输入：grid = [[1,2,3],[4,5,6],[7,8,9]\]
输出：35
解释：上图中的单元格表示元素总和最大的沙漏：1 + 2 + 3 + 5 + 7 + 8 + 9 = 35 。
 

提示：  
```
m == grid.length  
n == grid[i].length
3 <= m, n <= 150
0 <= grid[i][j] <= 106
```
### 思路
数据小,暴力模拟也能ac
这里用前缀和优化
```cpp
class Solution {
public:
    long long  b[153][153];
    int maxSum(vector<vector<int>>& grid) {
        memset(b,0,sizeof(b));
        for(int i=0;i<grid.size();i++){
            for(int j=0;j<grid[0].size();j++){
                b[i+1][j+1]=b[i][j+1]+b[i+1][j]+grid[i][j]-b[i][j];
            }
        }
        long long ans=-1;
        for(int i=3;i<=grid.size();i++){
            for(int j=3;j<=grid[0].size();j++){
                ans=max(ans,b[i][j] - b[i-3][j] - b[i][j-3] + b[i-3][j-3]-grid[i-2][j-3]-grid[i-2][j-1]);
            }
        }
        return ans;
                
    }
};
```
## T3 最小 XOR
给你两个正整数 num1 和 num2 ，找出满足下述条件的整数 x ：   

x 的置位数和 num2 相同，且
x XOR num1 的值 最小
注意 XOR 是按位异或运算。    

返回整数 x 。题目保证，对于生成的测试用例， x 是 唯一确定 的。   

整数的 置位数 是其二进制表示中 1 的数目。  

 

示例 1：
```
输入：num1 = 3, num2 = 5
输出：3
解释：
num1 和 num2 的二进制表示分别是 0011 和 0101 。
整数 3 的置位数与 num2 相同，且 3 XOR 3 = 0 是最小的。
```
示例 2：
```
输入：num1 = 1, num2 = 12
输出：3
解释：
num1 和 num2 的二进制表示分别是 0001 和 1100 。
整数 3 的置位数与 num2 相同，且 3 XOR 1 = 2 是最小的。
```

提示：
```
1 <= num1, num2 <= 109
```
### 思路
贪心+位运算
```cpp
class Solution {
public:
    int lowbit(int a){
        int cnt=0;
        while(a){
            a^=(a&(-a));
            cnt++;
        }
        return cnt;
    }
    int minimizeXor(int num1, int num2) {
        int cnt=lowbit(num2);
        int res=lowbit(num1);
        if(cnt==res)return num1;
        if(res>cnt){
            int dif=res-cnt;
            int ans=0;
            int p=num1;
            while(dif){
                dif--;
                ans+=num1&(-num1);
                num1^=(num1&(-num1));
            }
            return p-ans;
        }
        int d=-1;
        int t=cnt-res;
        int ans=0;
        while(d<31&&t>0){
            d++;
            if(num1&(1<<d)){continue;}
            ans+=pow(2,d);
            t--;
        }
        return ans+num1;
    }
};
```
### 缩减版
```cpp
class Solution {
public:
    int minimizeXor(int num1, int num2) {
        int c1 = __builtin_popcount(num1);
        int c2 = __builtin_popcount(num2);
        for (; c2 < c1; ++c2) num1 &= num1 - 1; // 最低的 1 变成 0
        for (; c2 > c1; --c2) num1 |= num1 + 1; // 最低的 0 变成 1
        return num1;
    }
};
// 作者：endlesscheng
```
## T4 对字母串可执行的最大删除数
```
给你一个仅由小写英文字母组成的字符串 s 。在一步操作中，你可以：

删除 整个字符串 s ，或者
对于满足 1 <= i <= s.length / 2 的任意 i ，如果 s 中的 前 i 个字母和接下来的 i 个字母 相等 ，删除 前 i 个字母。
例如，如果 s = "ababc" ，那么在一步操作中，你可以删除 s 的前两个字母得到 "abc" ，因为 s 的前两个字母和接下来的两个字母都等于 "ab" 。

返回删除 s 所需的最大操作数。
 


示例 1：

输入：s = "abcabcdabc"
输出：2
解释：
- 删除前 3 个字母（"abc"），因为它们和接下来 3 个字母相等。现在，s = "abcdabc"。
- 删除全部字母。
一共用了 2 步操作，所以返回 2 。可以证明 2 是所需的最大操作数。
注意，在第二步操作中无法再次删除 "abc" ，因为 "abc" 的下一次出现并不是位于接下来的 3 个字母。
示例 2：

输入：s = "aaabaab"
输出：4
解释：
- 删除第一个字母（"a"），因为它和接下来的字母相等。现在，s = "aabaab"。
- 删除前 3 个字母（"aab"），因为它们和接下来 3 个字母相等。现在，s = "aab"。 
- 删除第一个字母（"a"），因为它和接下来的字母相等。现在，s = "ab"。
- 删除全部字母。
一共用了 4 步操作，所以返回 4 。可以证明 4 是所需的最大操作数。
示例 3：

输入：s = "aaaaa"
输出：5
解释：在每一步操作中，都可以仅删除 s 的第一个字母。
 

提示：

1 <= s.length <= 4000
s 仅由小写英文字母组成
```
### 朴素记忆化搜索(MLE)
```py
class Solution:
    def deleteString(self, s: str) -> int:
        if len(set(s)) == 1: 
            return len(s)
        @cache
        def dfs(i,start):
            ans=0
            if i>=len(s):
                if i==start:
                    return 0
                return 1
            # print(s[start:i+1],s[i+1:i+1+(i+1-start)])
            if s[start:i+1]==s[i+1:i+1+(i+1-start)]:
                ans=dfs(i+1,i+1)+1
            ans=max(ans,dfs(i+1,start))
            return ans
        dfs.cache_clear()
        return dfs(0,0)  
```

### 朴素动态规划(TLE)
```py
class Solution:
    def deleteString(self, s: str) -> int:     
        size=len(s)+1
        dfs=[[0]*(size+2) for _ in range(size+2)]
        for j in range(size):
            if j==size-1:
                dfs[size-1][j]=0
            else:
                dfs[size-1][j]=1
        for i in range(size-1,-1,-1):
            for j in range(size-1,-1,-1):
                if s[j:i+1]==s[i+1:i+1+(i+1-j)]:
                    dfs[i][j]=dfs[i+1][i+1]+1
                dfs[i][j]=max(dfs[i][j],dfs[i+1][j])
        return dfs[0][0]
```

### LCP优化朴素动态规划(TLE)
```py
class Solution:
    def deleteString(self, s: str) -> int:
        size=len(s)+1
        if len(set(s)) == 1: return size-1
        dfs=[[0]*(size+2) for _ in range(size+2)]
        lcp=[[0]*(size+2) for _ in range(size+2)]
        for i in range(size-2, -1, -1):
            for j in range(size-2, i, -1):
                if s[i] == s[j]:
                    lcp[i][j] = lcp[i + 1][j + 1] + 1
        for j in range(size):
            if j==size-1:
                dfs[size-1][j]=0
            else:
                dfs[size-1][j]=1
        for i in range(size-1,-1,-1):
            for j in range(size-1,-1,-1):
                if lcp[j][i+1]>=i+1-j:
                    dfs[i][j]=dfs[i+1][i+1]+1
                dfs[i][j]=max(dfs[i][j],dfs[i+1][j])
        return dfs[0][0]
```



### 剪枝记忆化搜索(AC)
```py
class Solution:
    def deleteString(self, s: str) -> int:
        @cache
        def dfs(i):
            s_ = s[i:]
            ans = 1
            for j in range(1, len(s) // 2 + 1):
                if s_[:j] == s_[j:j*2]:
                    ans = max(ans, 1 + dfs(i + j))
            return ans
        
        dfs.cache_clear()
        return dfs(0)
```
### 剪枝+LCP优化动态规划(AC)
```py
class Solution:
    def deleteString(self, s: str) -> int:        
        n = len(s)
        if len(set(s)) == 1: return n  # 特判全部相同的情况
        lcp = [[0] * (n + 1) for _ in range(n + 1)]  # lcp[i][j] 表示 s[i:] 和 s[j:] 的最长公共前缀
        for i in range(n - 1, -1, -1):
            for j in range(n - 1, i, -1):
                if s[i] == s[j]:
                    lcp[i][j] = lcp[i + 1][j + 1] + 1
        f = [0] * n
        for i in range(n - 1, -1, -1):
            for j in range(1, (n - i) // 2 + 1):
                if lcp[i][i + j] >= j:  # 说明 s[i:i+j] == s[i+j:i+2*j]
                    f[i] = max(f[i], f[i + j])
            f[i] += 1
        return f[0]
# endlesscheng
```