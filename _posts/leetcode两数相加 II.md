---
title: 445. 两数相加 II (Add Two Numbers II)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [445\. 两数相加 II](https://leetcode-cn.com/problems/add-two-numbers-ii/)

Difficulty: **中等**


给你两个 **非空** 链表来代表两个非负整数。数字最高位位于链表开始位置。它们的每个节点只存储一位数字。将这两数相加会返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

**进阶：**

如果输入链表不能修改该如何处理？换句话说，你不能对列表中的节点进行翻转。

**示例：**

```
输入：(7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 8 -> 0 -> 7
```


#### Solution

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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        return reverse(addTwoNumbersLSB(reverse(l1),reverse(l2)));
    }
    
    public ListNode addTwoNumbersLSB(ListNode l1,ListNode l2){
        int carry = 0;
        ListNode dummyHead = new ListNode(0);
        ListNode curr = dummyHead;
        while(l1 !=null || l2 != null || carry != 0){
            int sum = (l1 == null ? 0: l1.val) + ( l2 == null ? 0:l2.val) + carry;
           
            ListNode node = new ListNode(sum % 10);
            carry = sum / 10;
            curr.next = node;
            curr = node;
            l1 = l1 == null ? null:l1.next;
            l2 = l2 == null ? null:l2.next;
        }
        return dummyHead.next;
    }
    
    public ListNode reverse(ListNode head){
        ListNode curr = head;
        ListNode prev = null;
        while(curr != null){
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        return prev;
    }
}
```

---
***参考：[leetcode](https://leetcode-cn.com/problems/add-two-numbers-ii/)***
