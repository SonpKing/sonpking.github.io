---
title: leetcode 103. 二叉树的锯齿形层序遍历
comments: true
categories: leetcode
tags: [队列]
date: 2020-12-9
---

## 题目
给定一个二叉树，返回其节点值的锯齿形层序遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

[原题链接](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal/)
## 题解
本题是层序遍历的变形，只需根据层数来判断每层的元素是从左到右还从右到左。

## 代码
```cpp 
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        queue<TreeNode*> que;
        if(root){
            que.push(root);
        }
        vector<vector<int>> res;
        while(!que.empty()){
            int n = que.size();
            vector<int> tmp;
            for(int i = 0; i < n; ++i){
                TreeNode* t = que.front();
                tmp.push_back(t->val);
                que.pop();
                if(t -> left){
                    que.push(t -> left);
                }
                if(t -> right){
                    que.push(t -> right);
                }
            }
            if(res.size()%2 == 1){
                reverse(tmp.begin(), tmp.end());
            }
            res.push_back(tmp);
        }
        return res;
    }
};
```

