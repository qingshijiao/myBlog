---
title: 328.奇偶链表 (Odd Even Linked List)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [328\. 奇偶链表](https://leetcode-cn.com/problems/odd-even-linked-list/)

Difficulty: **中等**


给定一个单链表，把所有的奇数节点和偶数节点分别排在一起。请注意，这里的奇数节点和偶数节点指的是节点编号的奇偶性，而不是节点的值的奇偶性。

请尝试使用原地算法完成。你的算法的空间复杂度应为 O(1)，时间复杂度应为 O(nodes)，nodes 为节点总数。

**示例 1:**

```
输入: 1->2->3->4->5->NULL
输出: 1->3->5->2->4->NULL
```

**示例 2:**

```
输入: 2->1->3->5->6->4->7->NULL
输出: 2->3->6->7->1->5->4->NULL
```

**说明:**

*   应当保持奇数节点和偶数节点的相对顺序。
*   链表的第一个节点视为奇数节点，第二个节点视为偶数节点，以此类推。


#### Solution
![](https://pic.leetcode-cn.com/00bd1d974b5a2e6d7d4faf0d5baad1c691f4ed8963cb1b7133d1112bad4c5e86-image.png)
Language: **Java**

```java
​public class Solution {
    public ListNode oddEvenList(ListNode head) {
        if (head == null) return null;
        ListNode odd = head, even = head.next, evenHead = even;
        while (even != null && even.next != null) {
            odd.next = even.next;
            odd = odd.next;
            even.next = odd.next;
            even = even.next;
        }
        odd.next = evenHead;
        return head;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/odd-even-linked-list/solution/qi-ou-lian-biao-by-leetcode/)***
