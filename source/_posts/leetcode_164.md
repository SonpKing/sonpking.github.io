---
title: leetcode 164. 最大间距
comments: true
categories: leetcode
tags: [C++, 题解, 排序]
date: 2020-11-26
---

## 题目
给定一个无序的数组，找出数组在排序之后，相邻元素之间最大的差值。  
如果数组元素个数小于 2，则返回 0。  
[原题链接](https://leetcode-cn.com/problems/maximum-gap/)

## 题解
要找出两个数的最大差值，那么就需要对原数组排序。最常见的快速排序的时间复杂度为NlgN。注意到题目中数值的范围为32位整数，所以考虑使用基数排序，时间复杂度仅为kN。
## 代码
快排
```cpp
class Solution {
public:
    int maximumGap(vector<int>& nums) {
        int n = nums.size();
        if(n < 2){
            return 0;
        }
        sort(nums.begin(), nums.end());
        int res = 0;
        for(int i = 1; i < n; ++i){
            if(nums[i] - nums[i-1] > res){
                res = nums[i] - nums[i-1];
            }
        }
        return res;
    }
};
```
基数排序
```cpp
class Solution {
public:
    int maximumGap(vector<int>& nums) {
        int n = nums.size();
        if(n < 2){
            return 0;
        }
        radix_sort(nums);
        int res = 0;
        for(int i = 1; i < n; ++i){
            if(nums[i] - nums[i-1] > res){
                res = nums[i] - nums[i-1];
            }
        }
        return res;
    }

    void radix_sort(vector<int>& nums){
        int n = nums.size();
        long long exp = 1; //最大的整数*10会越界，所以应当使用long long
        int maxv = *max_element(nums.begin(), nums.end());
        vector<int> tmp(n);
        int cnt[10] = {0};
        while(exp <= maxv){
            for(int i = 0; i < 10; ++i){
                cnt[i] = 0;
            }
            for(int i = 0; i < n; ++i){
                ++cnt[(nums[i]/exp)%10];
            }
            for(int i = 1; i < 10; ++i){
                cnt[i] += cnt[i-1];
            }
            for(int i = n-1; i >= 0; --i){
                tmp[--cnt[(nums[i]/exp)%10]] = nums[i];
            }
            swap(nums, tmp);
            exp *= 10;
        }
    }
};
```