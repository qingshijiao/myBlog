---
title: 234.回文链表（Palindrome Linked List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [234\. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

Difficulty: **简单**


请判断一个链表是否为回文链表。

**示例 1:**

```
输入: 1->2
输出: false
```

**示例 2:**

```
输入: 1->2->2->1
输出: true
```

**进阶：**
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？


#### Solution - 快慢指针

Language: **Java**

```java
​/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null) {
            return true;
        }
        ListNode slow = head, fast = head;
        ListNode pre = head, prepre = null;
        while(fast != null && fast.next != null) {
            pre = slow;
            slow = slow.next;
            fast = fast.next.next;
            pre.next = prepre;
            prepre = pre;
        }
        if(fast != null) {
            slow = slow.next;
        }
        while(pre != null && slow != null) {
            if(pre.val != slow.val) {
                return false;
            }
            pre = pre.next;
            slow = slow.next;
        }
        return true;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/palindrome-linked-list/submissions/)
[zhangbaipeng](https://leetcode-cn.com/problems/palindrome-linked-list/solution/kuai-man-zhi-zhen-he-dan-lian-biao-fan-zhuan-by-zh/)***
