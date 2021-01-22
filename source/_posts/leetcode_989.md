---
title: 989. 数组形式的整数加法
comments: true
categories: leetcode
tags: [大数]
date: 2021-1-22
---

## 题目

对于非负整数 X 而言，X 的数组形式是每位数字按从左到右的顺序形成的数组。例如，如果 X = 1231，那么其数组形式为 [1,2,3,1]。

给定非负整数 X 的数组形式 A，返回整数 X+K 的数组形式。

 

示例 1：
```
输入：A = [1,2,0,0], K = 34
输出：[1,2,3,4]
解释：1200 + 34 = 1234
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-to-array-form-of-integer

## 题解
大数加法的变形。首先把K转为整数数组（逆序），然后将A倒置。用t变量保存进位，遍历k和A进行大数相加。注意如果遍历完，t不为0，那么也要把它加入结果中。最后把结果数组倒置。

## 代码
```cpp 
class Solution {
public:
    vector<int> addToArrayForm(vector<int>& A, int K) {
        vector<int> k = convert(K);
        reverse(A.begin(), A.end());
        vector<int> res;
        int n = k.size(), m = A.size();
        int i = 0, j = 0;
        int t = 0;
        while(i < n || j < m){
            if(i < n){
                t += k[i++];
            }
            if(j < m){
                t += A[j++];
            }
            res.push_back(t % 10);
            t /= 10;
        }
        if(t > 0){
            res.push_back(t);
        }
        reverse(res.begin(), res.end());
        return res;
    }

    vector<int> convert(int K){
        vector<int> res;
        while(K){
            res.push_back(K % 10);
            K /= 10;
        }
        return res;
    }
};
```