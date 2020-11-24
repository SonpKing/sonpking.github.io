---
title: leetcode 222. 完全二叉树的节点个数
comments: true
categories: leetcode
tags: [C++, 题解, dfs, 二叉树]
---

## 题目
给出一个完全二叉树，求出该树的节点个数。  
说明：  
完全二叉树的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

示例:

输入: 
```
     1
    / \
   2   3
  / \  /
 4  5 6
```
输出: 6
## 题解
完全二叉树的编号非常有规律，若父节点编号为N，那么左子节点的编号为2\*N，右子节点的编号为2\*N+1。我们的目标是找到树中所有节点的个数，如果根节点编号为1，那么我们要找的就是最后一个节点的编号。如何判断最后一个节点在左子树还是右子树呢？一个比较简单的方法是看左右子树树高，如果相等那么最后一个节点必然在右子树，否则在左子树。
## 代码
```cpp 
class Solution {
public:
    int countNodes(TreeNode* root) {
        if(root == nullptr){
            return 0;
        }else{
            return recur(root, 1);
        }
    }
    
    int recur(TreeNode* root, int num){
        if(!root->left && !root->right){
            return num;
        }
        int left = getHeight(root -> left);
        int right = getHeight(root -> right);
        if(left == right){
            return recur(root -> right, 2*num + 1);
        }else{
            return recur(root -> left, 2*num);
        }    
    }

    int getHeight(TreeNode* root) {
        int cnt = 0;
        while(root){
            ++cnt;
            root = root -> left;
        }
        return cnt;
    }
};
```