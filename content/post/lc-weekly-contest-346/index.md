---
title: lc weekly contest 346 
description: 本场竞赛由「顺丰科技 & 力扣」联合主办
slug: lc-weekly-contest-346 
date: 2023-05-21 00:00:00+0000
tags:
    - Leetcode
image: https://pic.lingkou.xyz/1684119642-NLFpUC-1760-360%20%E9%A1%BA%E4%B8%B0%E7%A7%91%E6%8A%80.png
---
## 写在前面
> [LC346传送门](https://leetcode.cn/contest/weekly-contest-346/)
第四题难,前三题难度较低
## T1 删除子串后的字符串最小长度
给你一个仅由 大写 英文字符组成的字符串 s 。
你可以对此字符串执行一些操作，在每一步操作中，你可以从 s 中删除 任一个 "AB" 或 "CD" 子字符串。
通过执行操作，删除所有 "AB" 和 "CD" 子串，返回可获得的最终字符串的 最小 可能长度。
注意，删除子串后，重新连接出的字符串可能会产生新的 "AB" 或 "CD" 子串
### 示例 1：

输入：s = "ABFCACDB"
输出：2
解释：你可以执行下述操作：
- 从 "ABFCACDB" 中删除子串 "AB"，得到 s = "FCACDB" 。
- 从 "FCACDB" 中删除子串 "CD"，得到 s = "FCAB" 。
- 从 "FCAB" 中删除子串 "AB"，得到 s = "FC" 。
最终字符串的长度为 2 。
可以证明 2 是可获得的最小长度。  
### 示例 2：

输入：s = "ACBBD"
输出：5
解释：无法执行操作，字符串长度不变。
### 思路
模拟/栈(类似括号删除)
### 比赛代码(模拟)
```py
class Solution:
    def minLength(self, s: str) -> int:
        p1=0
        p2=1
        if len(s)==1:
            return 1
        a=[]
        for i in s:
            a.append(i)
        while p2<len(a):
            if a[p1]=="A" and a[p2]=="B":
                del a[p1]
                del a[p2-1]
                if p1!=0 and p2!=1:
                    p1-=1
                    p2-=1
            elif a[p1]=="C" and a[p2]=="D":
                del a[p1]
                del a[p2-1]
                if p1!=0 and p2!=1:
                    p1-=1
                    p2-=1
            else:
                p1+=1
                p2+=1
        return len(a)
```
### 语法糖模拟
```py
class Solution:
    def minLength(self, s: str) -> int:
        while "AB" in s or "CD" in s:
            s = s.replace("AB", "").replace("CD", "")
        return len(s)
# 作者：endlesscheng
```
### 栈
```cpp
class Solution {
public:
    int minLength(string s) {
        stack<char> ss;
        for(auto i:s){
            if(!ss.empty()&&((ss.top()=='A'&&i=='B')||(ss.top()=='C'&&i=='D')))ss.pop();
            else ss.push(i);
        }
        return ss.size();
    }
};
```
## T2 字典序最小回文串
给你一个由 小写英文字母 组成的字符串 s ，你可以对其执行一些操作。在一步操作中，你可以用其他小写英文字母 替换  s 中的一个字符。

请你执行 尽可能少的操作 ，使 s 变成一个 回文串 。如果执行 最少 操作次数的方案不止一种，则只需选取 字典序最小 的方案。

对于两个长度相同的字符串 a 和 b ，在 a 和 b 出现不同的第一个位置，如果该位置上 a 中对应字母比 b 中对应字母在字母表中出现顺序更早，则认为 a 的字典序比 b 的字典序要小。

返回最终的回文字符串。

 

示例 1：

输入：s = "egcfe"
输出："efcfe"
解释：将 "egcfe" 变成回文字符串的最小操作次数为 1 ，修改 1 次得到的字典序最小回文字符串是 "efcfe"，只需将 'g' 改为 'f' 。
示例 2：

输入：s = "abcd"
输出："abba"
解释：将 "abcd" 变成回文字符串的最小操作次数为 2 ，修改 2 次得到的字典序最小回文字符串是 "abba" 。
示例 3：

输入：s = "seven"
输出："neven"
解释：将 "seven" 变成回文字符串的最小操作次数为 1 ，修改 1 次得到的字典序最小回文字符串是 "neven" 。
 

提示：

1 <= s.length <= 1000
s 仅由小写英文字母组成

### 思路
双指针
### 赛时代码
```cpp
class Solution {
public:
    string makeSmallestPalindrome(string s) {
        int st=0;
        int ed=s.size()-1;
        while(st<ed){
            if(s[st]!=s[ed]){
                if(s[st]-'a'>s[ed]-'a'){
                    s[st]=s[ed];
                }
                else{
                    s[ed]=s[st];
                }
            }
            st++;
            ed--;
        }
        return s;
    }
};
```
## T3 求一个整数的惩罚数
给你一个正整数 n ，请你返回 n 的 惩罚数 。

n 的 惩罚数 定义为所有满足以下条件 i 的数的平方和：

1 <= i <= n
i * i 的十进制表示的字符串可以分割成若干连续子字符串，且这些子字符串对应的整数值之和等于 i 。
 
  
示例 1：

输入：n = 10
输出：182
解释：总共有 3 个整数 i 满足要求：
- 1 ，因为 1 * 1 = 1
- 9 ，因为 9 * 9 = 81 ，且 81 可以分割成 8 + 1 。
- 10 ，因为 10 * 10 = 100 ，且 100 可以分割成 10 + 0 。
因此，10 的惩罚数为 1 + 81 + 100 = 182   
示例 2：

输入：n = 37
输出：1478
解释：总共有 4 个整数 i 满足要求：
- 1 ，因为 1 * 1 = 1
- 9 ，因为 9 * 9 = 81 ，且 81 可以分割成 8 + 1 。
- 10 ，因为 10 * 10 = 100 ，且 100 可以分割成 10 + 0 。
- 36 ，因为 36 * 36 = 1296 ，且 1296 可以分割成 1 + 29 + 6 。
因此，37 的惩罚数为 1 + 81 + 100 + 1296 = 1478
 

提示：

1 <= n <= 1000
### 思路
比赛时看到n最大才1000,可以直接预处理
打表用的dfs, 为了节约时间没把dfs改成动态规划
### 赛时代码
```py
# 打表代码
# a=[]
# s=""
# def check(i,v,p):
#     if i>=len(s):
#         if p==v:
#             return 1
#         return 0
#     x=0
#     for d in range(i,len(s)):
#         x=x|check(d+1,v,p+int(s[i:d+1]))
#     return x
    
# for i in range(1,1001):
#     s=str(i*i)
#     if check(0,i,0):
#         a.append(i)
# print(a)
class Solution:
    def punishmentNumber(self, n: int) -> int:
        s={1, 9, 10, 36, 45, 55, 82, 91, 99, 100, 235, 297, 369, 370, 379, 414, 657, 675, 703, 756, 792, 909, 918, 945, 964, 990, 991, 999, 1000}
        cnt=0
        for i in range(1,n+1):
            if i in s:
                cnt+=i*i
        return cnt
```
### 记忆化搜索
```py
class Solution:
    def punishmentNumber(self, n: int) -> int:
        @cache
        def check(i,v,p,s):
            if i>=len(s):
                if p==v:
                    return 1
                return 0
            x=0
            for d in range(i,len(s)):
                x=x|check(d+1,v,p+int(s[i:d+1]),s)
            return x
        cnt=0
        for i in range(1,n+1):
            s=str(i*i)
            if check(0,i,0,s):
                cnt+=i*i
        return cnt
```
## T4修改图中的边权
给你一个 n 个节点的 无向带权连通 图，节点编号为 0 到 n - 1 ，再给你一个整数数组 edges ，其中 edges[i] = [ai, bi, wi] 表示节点 ai 和 bi 之间有一条边权为 wi 的边。

部分边的边权为 -1（wi = -1），其他边的边权都为 正 数（wi > 0）。

你需要将所有边权为 -1 的边都修改为范围 [1, 2 * 109] 中的 正整数 ，使得从节点 source 到节点 destination 的 最短距离 为整数 target 。如果有 多种 修改方案可以使 source 和 destination 之间的最短距离等于 target ，你可以返回任意一种方案。

如果存在使 source 到 destination 最短距离为 target 的方案，请你按任意顺序返回包含所有边的数组（包括未修改边权的边）。如果不存在这样的方案，请你返回一个 空数组 。

注意：你不能修改一开始边权为正数的边。

示例 1：

输入：n = 5, edges = [[4,1,-1],[2,0,-1],[0,3,-1],[4,3,-1]\], source = 0, destination = 1, target = 5
输出：[[4,1,1],[2,0,1],[0,3,3],[4,3,1]\]
解释：上图展示了一个满足题意的修改方案，从 0 到 1 的最短距离为 5 。
示例 2：



输入：n = 3, edges = [[0,1,-1],[0,2,5]\], source = 0, destination = 2, target = 6
输出：[]
解释：上图是一开始的图。没有办法通过修改边权为 -1 的边，使得 0 到 2 的最短距离等于 6 ，所以返回一个空数组。
示例 3：



输入：n = 4, edges = [[1,0,4],[1,2,3],[2,3,5],[0,3,-1]\], source = 0, destination = 2, target = 6
输出：[[1,0,4],[1,2,3],[2,3,5],[0,3,1]\]
解释：上图展示了一个满足题意的修改方案，从 0 到 2 的最短距离为 6 。
 

提示：
```
1 <= n <= 100
1 <= edges.length <= n * (n - 1) / 2
edges[i].length == 3
0 <= ai, bi < n
wi = -1 或者 1 <= wi <= 107
ai != bi
0 <= source, destination < n
source != destination
1 <= target <= 109
输入的图是连通图，且没有自环和重边。
```
### 请见
{{< bilibili BV1Qm4y1t7cx >}}
