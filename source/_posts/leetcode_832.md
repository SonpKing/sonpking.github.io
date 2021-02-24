---
title: leetcode 832. 翻转图像
comments: true
categories: leetcode
tags: [双指针, 字符串]
date: 2021-02-24
---

## 题目
给定一个二进制矩阵 A，我们想先水平翻转图像，然后反转图像并返回结果。

水平翻转图片就是将图片的每一行都进行翻转，即逆序。例如，水平翻转 [1, 1, 0] 的结果是 [0, 1, 1]。

反转图片的意思是图片中的 0 全部被 1 替换， 1 全部被 0 替换。例如，反转 [0, 1, 1] 的结果是 [1, 0, 0]。

示例 1：
```
输入：[[1,1,0],[1,0,1],[0,0,0]]
输出：[[1,0,0],[0,1,0],[1,1,1]]
解释：首先翻转每一行: [[0,1,1],[1,0,1],[0,0,0]]；
     然后反转图片: [[1,0,0],[0,1,0],[1,1,1]]
```
来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/flipping-an-image

## 题解
调用库函数reverse()把每行反转，库函数使用的是双指针法从两边向中间遍历。接着反转每个数字，因为只有0和1，所以用1减去原数就得到反转后的数字。

## 代码
```cpp 
class Solution {
public:
    vector<vector<int>> flipAndInvertImage(vector<vector<int>>& A) {
        int n = A.size();
        int m = A[0].size();
        for(int i = 0; i < n; ++i){
            reverse(A[i].begin(), A[i].end());
            for(int j = 0; j < m; ++j){
                A[i][j] = 1 - A[i][j];
            }
        }
        return A;
    }
};
```