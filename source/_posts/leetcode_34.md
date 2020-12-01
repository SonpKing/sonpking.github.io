---
title: leetcode 34. 在排序数组中查找元素的第一个和最后一个位置
comments: true
categories: leetcode
tags: [二分]
date: 2020-12-1
mathjax: true
---

## 题目
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

[原题链接](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)
## 题解
根据题意，最直观的做法是从前往后遍历一遍。但是这种做法的平均时间复杂度为$O(n)$。在有序数组中查找的最快算法是二分法，参考库函数lower_bound()，我们定义一个找到第一个大于等于target的函数，这样就找到了左边界。再次利用这个函数找第一个大于等于target+1的函数，这样就找到了右边界，注意需要减一。二分法的时间复杂度为$O(lgN)$。
## 代码
```cpp 
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int start = lowerbound(nums, target);
        int end = lowerbound(nums, target + 1);
        if(start == end){
            return vector<int>{-1, -1};
        }else{
            return vector<int>{start, end - 1};
        }
    }

    int lowerbound(vector<int>& nums, int target){
        int i = 0, j = nums.size() - 1;
        while(i <= j){
            int m = i + (j - i) / 2;
            if(nums[m] >= target){
                j = m - 1;
            }else{
                i = m + 1;
            }
        }
        return i;
    }
};
```