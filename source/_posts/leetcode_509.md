---
title: leetcode 509. 斐波那契数
comments: true
categories: leetcode
tags: [动态规划]
date: 2021-01-04
---

## 题目
斐波那契数，通常用 F(n) 表示，形成的序列称为 斐波那契数列 。该数列由 0 和 1 开始，后面的每一项数字都是前面两项数字的和。也就是：

F(0) = 0，F(1) = 1
F(n) = F(n - 1) + F(n - 2)，其中 n > 1
给你 n ，请计算 F(n) 。

示例 1：
```
输入：2
输出：1
解释：F(2) = F(1) + F(0) = 1 + 0 = 1
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fibonacci-number

## 题解
题中已经给出了递推方程，只需要正序计算n为1,2,3,...,n的值。

## 代码
```cpp 
class Solution {
public:
    int fib(int n) {
        int f0 = 0, f1 = 1, f2 = -1;
        if(n == 0){
            return 0;
        }
        for(int i = 1; i < n; ++i){
            f2 = f0 + f1;
            f0 = f1;
            f1 = f2;
        }
        return f1;
    }
};
```