---
title: 237.删除链表中的节点（Delete Node in a Linked List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [237\. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

Difficulty: **简单**


请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点，你将只被给定要求被删除的节点。

现有一个链表 -- head = [4,5,1,9]，它可以表示为:

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/01/19/237_example.png)

**示例 1:**

```
输入: head = [4,5,1,9], node = 5
输出: [4,1,9]
解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
```

**示例 2:**

```
输入: head = [4,5,1,9], node = 1
输出: [4,5,9]
解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.
```

**说明:**

*   链表至少包含两个节点。
*   链表中所有节点的值都是唯一的。
*   给定的节点为非末尾节点并且一定是链表中的一个有效节点。
*   不要从你的函数中返回任何结果。


#### Solution - 与下一个节点交换
![](https://pic.leetcode-cn.com/858fae01d89c2080eb7e45a1f9d9a2b2f76e1a5c87815b324fd946e0bd8da495-file_1555866651920)
![](https://pic.leetcode-cn.com/902dc5d3f8c44d3cbc0b6e837711cad2eefc021fd2b9de8dfabc6d478bc779b1-file_1555866680932)
![](https://pic.leetcode-cn.com/2a6409b98dd73d6649fdc6fb984c88690547127467104c3923367be6f8fbc916-file_1555866773685)

Language: **Java**

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public void deleteNode(ListNode node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/solution/shan-chu-lian-biao-zhong-de-jie-dian-by-leetcode/)***
