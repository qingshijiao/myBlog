---
title: 24. 两两交换链表中的节点（Swap Nodes in Pairs）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

示例:

> 给定 1->2->3->4, 你应该返回 2->1->4->3.



# 题解

## 官方题解
暂无

## 其他题解
### 1.递归
**思路：**
- 返回值：交换完成的子链表
- 调用单元：设需要交换的两个点为 head 和 next，head 连接后面交换完成的子链表，next 连接 head，完成交换
- 终止条件：head 为空指针或者 next 为空指针，也就是当前无节点或者只有一个节点，无法进行交换

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
 class Solution {
     public ListNode swapPairs(ListNode head) {
         if(head == null || head.next == null){
             return head;
         }
         ListNode n = head.next;
         head.next = swapPairs(n.next);
         n.next = head;
         return n;
     }
 }
```
**复杂度分析**

### 2.非递归
**思路：**

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
 class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode pre = new ListNode(0);
        pre.next = head;
        ListNode temp = pre;
        while(temp.next != null && temp.next.next != null) {
            ListNode start = temp.next;
            ListNode end = temp.next.next;
            temp.next = end;
            start.next = end.next;
            end.next = start;
            temp = start;
        }
        return pre.next;
    }
}
```
**复杂度分析**



---
***参考：
[guanpengchn](https://leetcode-cn.com/problems/swap-nodes-in-pairs/solution/hua-jie-suan-fa-24-liang-liang-jiao-huan-lian-biao/)***
