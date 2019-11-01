---
title: 147.对链表进行插入排序（Insertion Sort List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
对链表进行插入排序。

![](https://upload.wikimedia.org/wikipedia/commons/0/0f/Insertion-sort-example-300px.gif)
插入排序的动画演示如上。从第一个元素开始，该链表可以被认为已经部分排序（用黑色表示）。
每次迭代时，从输入数据中移除一个元素（用红色表示），并原地将其插入到已排好序的链表中。

 

插入排序算法：

- 插入排序是迭代的，每次只移动一个元素，直到所有元素可以形成一个有序的输出列表。
- 每次迭代中，插入排序只从输入数据中移除一个待排序的元素，找到它在序列中适当的位置，并将其插入。
- 重复直到所有输入数据插入完为止。
 

示例 1：
```
输入: 4->2->1->3
输出: 1->2->3->4
```
示例 2：
```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.添加哑节点和尾节点

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
    public ListNode insertionSortList(ListNode head) {
        ListNode dummy = new ListNode(Integer.MIN_VALUE);
        ListNode pre = dummy;
        ListNode tail = dummy;
        ListNode cur = head;
        while (cur != null) {
            if (tail.val < cur.val) {
                tail.next = cur;
                tail = cur;
                cur = cur.next;
            } else {
                ListNode tmp = cur.next;
                tail.next = tmp;
                while (pre.next != null && pre.next.val < cur.val) pre = pre.next;
                cur.next = pre.next;
                pre.next = cur;
                pre = dummy;
                cur = tmp;
            }
        }
        return dummy.next;
    }
}
```

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
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        // (dummy) -> (4/head) -> (2) -> (1) -> (3)

        while (head != null && head.next != null) {
            if (head.val < head.next.val) {
                head = head.next;
                continue;
            }

            ListNode p = dummy;
            // (dummy/p) -> (4/head) -> (2) -> (1) -> (3)

            while (p.next.val < head.next.val) {
                p = p.next;
            }
            // (dummy/p) -> (4/head) -> (2) -> (1) -> (3)

            ListNode t = head.next;
            head.next = head.next.next;
            t.next = p.next;
            p.next = t;

            // (dummy) -> (2/p) -> (4/head) -> (1) -> (3)
        }
        return dummy.next;
    }
}
```

### 2.分治
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
    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode left = head;
        ListNode right = head.next;
        while (right != null && right.next != null) {
            left = left.next;
            right = right.next.next;
        }
        right = left.next;
        left.next = null;
        ListNode result = new ListNode(0);
        ListNode resultHead = result;
        ListNode leftNode = insertionSortList(head);
        ListNode rightNode = insertionSortList(right);
        while (leftNode != null && rightNode != null) {
            if (leftNode.val < rightNode.val) {
                result.next = leftNode;
                result = result.next;
                leftNode = leftNode.next;
            } else {
                result.next = rightNode;
                result = result.next;
                rightNode = rightNode.next;
            }
        }
        result.next = leftNode == null ? rightNode : leftNode;
        return resultHead.next;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/insertion-sort-list/)
[powcai](https://leetcode-cn.com/problems/insertion-sort-list/solution/jia-ge-tailsu-du-jiu-kuai-liao-by-powcai/)***
