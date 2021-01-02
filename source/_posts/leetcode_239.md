---
title: leetcode 239. 滑动窗口最大值
comments: true
categories: leetcode
tags: [单调栈]
date: 2021-1-2
---

## 题目

给你一个整数数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

示例 1：
```
输入：nums = [1,3,-1,-3,5,3,6,7], k = 3
输出：[3,3,5,5,6,7]
解释：
滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
```

[原题链接](https://leetcode-cn.com/problems/sliding-window-maximum)
## 题解
用一个单调下降的栈保存窗口最大值。每当窗口向后移动一步，首先比较这个值和栈顶的值，如果比栈顶大那么则弹出栈顶元素，否则加入栈中。然后比较栈底的值和窗口左侧的值，如果相等则弹出栈底的值。虽然这里称做栈，其实包含的操作是双端队列的操作，所以选择C++库中的deque容器实现。

## 代码
```cpp 
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        deque<int> que;
        vector<int> res;
        for(int i = 0; i < n; ++i){
            while(!que.empty() && que.back() < nums[i]){
                que.pop_back();
            }
            que.push_back(nums[i]);
            if(i >= k - 1){
                res.push_back(que.front());
                if(nums[i-k+1] == que.front()){
                    que.pop_front();
                }
            }
        }
        return res;
    }
};
```