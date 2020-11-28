---
title: leetcode 493. 翻转对
comments: true
categories: leetcode
tags: [二分, 树状数组]
date: 2020-11-28
---

## 题目
给定一个数组 nums ，如果 i < j 且 nums[i] > 2*nums[j] 我们就将 (i, j) 称作一个重要翻转对。

你需要返回给定数组中的重要翻转对的数量。

[原题链接](https://leetcode-cn.com/problems/reverse-pairs/)
## 题解
本题和逆序对很相似，也可以使用归并算法的思想解决。不过在逆序对题中，统计逆序对的个数和merge的过程是放在一起的，而本题中需要先求翻转对的个数再排序。归并算法分为两步，第一步将原数组划分二等份，第二部合并。在合并过程中添加一些判断条件，就可以统计翻转对的个数。因为排序完成的那部分的翻转对的个数已经被统计过了，只需要关心未合并两部分之间存在的翻转对。
## 代码
```cpp 
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        int res = 0;
        vector<int> aux(nums.size());
        mergesort(nums, aux, 0, nums.size(), res);
        return res;
    }

    void mergesort(vector<int>& nums, vector<int>& aux, int start, int end, int &cnt){
        if(start + 1 >= end){
            return ;
        }
        int mid = start + (end - start) / 2;
        mergesort(nums, aux, start, mid, cnt);
        mergesort(nums, aux, mid, end, cnt);
        int i = start, j = mid;
        while(i < mid && j < end){
            if((long long)nums[i] > 2 * (long long)nums[j]){ //2 * nums[j] out of the range of integer
                cnt += mid - i; //all index > i will let nums[index] > 2 * nums[j]
                ++j;
            }else{
                ++i;
            }
        }
        
        i = start, j = mid;
        int t = start;
        while(i < mid && j < end){
            if(nums[i] <= nums[j]){
                aux[t++] = nums[i++];
            }else{
                aux[t++] = nums[j++];
            }
        }
        while(i < mid){
            aux[t++] = nums[i++];
        }
        while(j < end){
            aux[t++] = nums[j++];
        }
        for(t = start; t < end; ++t){
            nums[t] = aux[t];
        }
    }
};
```