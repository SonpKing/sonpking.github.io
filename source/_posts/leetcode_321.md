---
title: leetcode 321. 拼接最大数
comments: true
categories: leetcode
tags: [单调栈, 双指针]
date: 2020-12-2
---

## 题目
给定长度分别为 m 和 n 的两个数组，其元素由 0-9 构成，表示两个自然数各位上的数字。现在从这两个数组中选出 k (k <= m + n) 个数字拼接成一个新的数，要求从同一个数组中取出的数字保持其在原数组中的相对顺序。

求满足该条件的最大数。结果返回一个表示该最大数的长度为 k 的数组。

[原题链接](https://leetcode-cn.com/problems/create-maximum-number/)
## 题解
如果仅从一个数组中取出K个数并保持相对顺序不变，那么可以利用单调栈的思想。在满足个数的前提下，如果可以当前的数比栈顶大则更新栈顶。如何保证个数足够呢，需要用两个变量分别记录剩余的数字个数和需要数字个数。剩余个数在每一次循环后减1，需要的个数在入栈时减1，出栈时加1。现在来看两个数组的情况，我们把K个数拆分i和K-i，即在第一个数组中取i个数，第二个数组中取K-i个数。那么现在问题的关键是如何合并两个数组中得到的子序列。这里使用双指针的做法，比较两个指针当前指向数的大小，每次取大的那个指针更新。如果两指针指向的值相等，则继续比较后面的值。如果在比较的过程中一个数组遍历完了，则默认没有遍历完的数组更大。
## 代码
```cpp 
class Solution {
public:
    vector<int> maxNumber(vector<int>& nums1, vector<int>& nums2, int k) {
        int n = nums1.size();
        int m = nums2.size();
        vector<int> res, tmp;
        for(int i = max(0, k - m), maxi = min(n, k); i <= maxi; ++i){
            vector<int> t1 = get_subseq(nums1, i);
            vector<int> t2 = get_subseq(nums2, k - i);
            tmp = merge(t1, t2);
            if(cmp(tmp, res)){
                res.swap(tmp);
            }
        }
        return res;
    }

    bool cmp(vector<int>& nums1, vector<int>& nums2, int i = 0, int j = 0){
        int n = nums1.size(), m = nums2.size();
        while(i < n && j < m){
            if(nums1[i] < nums2[j]){
                return false;
            }else if(nums1[i] > nums2[j]){
                return true;
            }
            ++i;
            ++j;
        }
        return i < n;
    }

    vector<int> merge(vector<int>& nums1, vector<int>& nums2){
        vector<int> res;
        int n = nums1.size(), m = nums2.size();
        int i = 0, j = 0;
        while(i < n && j < m){
            if(nums1[i] > nums2[j]){
                res.push_back(nums1[i++]);
            }else if(nums1[i] < nums2[j]){
                res.push_back(nums2[j++]);
            }else if(cmp(nums1, nums2, i, j)){
                res.push_back(nums1[i++]);
            }else{
                res.push_back(nums2[j++]);
            }
        }
        while(i < n){
            res.push_back(nums1[i++]);
        }
        while(j < m){
            res.push_back(nums2[j++]);
        }
        return res;
    }

    vector<int> get_subseq(vector<int>& nums, int cnt){
        int n = nums.size();
        vector<int> stk;
        int remain = n;
        for(int i = 0; i < n; ++i){
            while(!stk.empty() && nums[i] > stk.back() && remain > cnt){
                stk.pop_back();
                ++cnt;
            }
            if(cnt > 0){
               stk.push_back(nums[i]); 
               --cnt;
            }
            --remain;
        }
        return stk;
    }
};
```

顺便复习一下字典序比较大小，本题暂不需要字典序这么严格的比较。
```cpp
bool cmp_dict(vector<int>& nums1, vector<int>& nums2, int i = 0, int j = 0){
    vector<int>::iterator it1 = nums1.begin() + i;
    vector<int>::iterator it2 = nums2.begin() + j;
    while(it1 != nums2.end() && it2 != nums1.end()){
        if(it1 == nums1.end()){
            it1 = nums2.begin() + j;
        }
        if(it2 == nums2.end()){
            it2 = nums1.begin() + i;
        }
        if(*it1 > *it2){
            return true;
        }else if(*it1 < *it2){
            return false;
        }
        ++it1;
        ++it2;
    }
    return true;
}
```