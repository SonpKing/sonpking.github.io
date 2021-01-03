---
title: leetcode 86. 分隔链表
comments: true
categories: leetcode
tags: [链表]
date: 2021-1-3
---

## 题目

给你一个链表和一个特定值 x ，请你对链表进行分隔，使得所有小于 x 的节点都出现在大于或等于 x 的节点之前。

你应当保留两个分区中每个节点的初始相对位置。

示例：
```
输入：head = 1->4->3->2->5->2, x = 3
输出：1->2->2->4->3->5
```

[原题链接](https://leetcode-cn.com/problems/partition-list)
## 题解
因为要保持分区内部的每个节点的相对位置，所以不能使用类似快排的partition方法（可能会乱序）。借助两个链表，遍历原始链表，如果当前节点的值比目标值小则加入第一个链表，否则加入第二个链表。注意第二个链表的最后一个节点的next值必须置空。

## 代码
```cpp 
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        ListNode *small = new ListNode(0);
        ListNode *large = new ListNode(0);
        ListNode *l1 = small, *l2 = large;
        while(head){
            if(head -> val < x){
                l1 -> next = head;
                l1 = l1 -> next;
            }else{
                l2 -> next = head;
                l2 = l2 -> next;
            }
            head  = head -> next;
        }
        l2 -> next = nullptr;
        l1 -> next = large -> next;
        return small -> next;
    }
};
```