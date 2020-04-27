---
title: 382.链表随机节点 (Linked List Random Node)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [382\. 链表随机节点](https://leetcode-cn.com/problems/linked-list-random-node/)

Difficulty: **中等**


给定一个单链表，随机选择链表的一个节点，并返回相应的节点值。保证每个节点**被选的概率一样**。

**进阶:**
如果链表十分大且长度未知，如何解决这个问题？你能否使用常数级空间复杂度实现？

**示例:**

```
// 初始化一个单链表 [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);

// getRandom()方法应随机返回1,2,3中的一个，保证每个元素被返回的概率相等。
solution.getRandom();
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
    int size;
    Random random;
    ListNode head;

    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        this.random = new Random();
        this.head = head;
        while (head != null) {
            this.size++;
            head = head.next;
        }
    }

    /** Returns a random node's value. */
    public int getRandom() {
        int k = random.nextInt(size);
        ListNode temp = head;
        while (k > 0) {
            temp = temp.next;
            k--;
        }
        return temp.val;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(head);
 * int param_1 = obj.getRandom();
 */
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/linked-list-random-node/submissions/)***
