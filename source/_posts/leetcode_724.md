---
title: leetcode 724. 寻找数组的中心索引
comments: true
categories: leetcode
tags: [双指针]
date: 2021-01-28
---

## 题目
给定一个整数类型的数组 nums，请编写一个能够返回数组 “中心索引” 的方法。

我们是这样定义数组 中心索引 的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。

如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。

 

示例 1：
```
输入：
nums = [1, 7, 3, 6, 5, 6]
输出：3
解释：
索引 3 (nums[3] = 6) 的左侧数之和 (1 + 7 + 3 = 11)，与右侧数之和 (5 + 6 = 11) 相等。
同时, 3 也是第一个符合要求的中心索引。
```

## 题解
用两个变量分别记录左半部分和右半部分的和，然后从左向右遍历，比较是够相等。如果相等则返回结果。如果遍历完成还没有的相等的，则返回-1。

## 代码
```cpp 
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int sum2 = 0;
        int n = nums.size();
        for(int i = n - 1; i >= 0; --i){
             sum2 += nums[i];
        }

        int sum1 = 0;
        for(int i = 0; i < n; ++i){
            sum2 -= nums[i];
            if(sum1 == sum2){
                return i;
            }
            sum1 += nums[i];
        }
        return -1;
    }
};
```