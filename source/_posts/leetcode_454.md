---
title: leetcode 454. 四数相加 II
comments: true
categories: leetcode
tags: [哈希表]
date: 2020-11-27
---

## 题目
给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -228 到 228 - 1 之间，最终结果不会超过 231 - 1 。

[原题链接](https://leetcode-cn.com/problems/4sum-ii/)
## 题解
因为只有4个数组，所以可以两两组成一组，此时时间复杂度已经为O(N^2)。利用字典我们可以在O(1)时间复杂度里，找到目标值。在本次中如果前两组数据的和为后两组数据和为M，那么我们需要在前两组的数据中找到和为-M的元组的个数，也就是说需要为前两组数据的枚举和做个数统计，并存放在字典中。
## 代码
```cpp 
class Solution {
public:
    int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        int n = A.size();
        unordered_map<int, int> cnt;
        for(int i = 0; i < n; ++i){
            for(int j = 0; j < n; ++j){
                ++cnt[(A[i] + B[j])];
            }
        }
        int res = 0;
        for(int i = 0; i < n; ++i){
            for(int j = 0; j < n; ++j){
                if(cnt.find(-(C[i] + D[j])) != cnt.end()){
                    res += cnt[-(C[i] + D[j])];
                }
            }
        }
        return res;
    }
};
```