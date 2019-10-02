---
title: 82.删除排序链表中的重复元素 II (Remove Duplicates from Sorted List II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:
```
输入: 1->2->3->3->4->4->5
输出: 1->2->5
```
示例 2:
```
输入: 1->1->1->2->3
输出: 2->3
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.迭代
**思想：** 快慢指针,用快指针跳过那些有重复数组,慢指针负责和快指针拼接!

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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return head;
        ListNode dummy = new ListNode(-1000);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy.next;
        while (fast != null) {
            while (fast.next != null && fast.val == fast.next.val) fast = fast.next;
            if (slow.next == fast) slow = slow.next;
            else slow.next = fast.next;
            fast = fast.next;
        }
        return dummy.next;
    }
}
```


### 2.递归
**思想：**

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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null)  return head;
        if (head.next != null && head.val == head.next.val) {
            while (head.next != null && head.val == head.next.val) {
                head = head.next;
            }
            return deleteDuplicates(head.next);
        }
        else head.next = deleteDuplicates(head.next);
        return head;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/submissions/)
[powcai](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/solution/kuai-man-zhi-zhen-by-powcai-2/)***
