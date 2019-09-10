---
title: 25. K 个一组翻转链表（Reverse Nodes in k-Group）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。

k 是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

示例 :
> 给定这个链表：1->2->3->4->5
> 当 k = 2 时，应当返回: 2->1->4->3->5
> 当 k = 3 时，应当返回: 3->2->1->4->5

说明 :
> 你的算法只能使用常数的额外空间。
> 你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

# 题解

## 官方题解
暂无

## 其他题解
### 1.非递归
**思路：**
![](https://i.loli.net/2019/09/06/WF7bTqa6EK2QmnV.png)
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
    public ListNode reverseKGroup(ListNode head, int k) {
        //哑节点
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode pre = dummy;
        ListNode end = dummy;

        while (end.next != null) {
            //判断是否能构成一组
            for (int i = 0; i < k && end != null; i++) end = end.next;
            if (end == null) break;
            //成组逆转
            ListNode start = pre.next;
            ListNode next = end.next;
            end.next = null;
            pre.next = reverse(start);
            start.next = next;
            pre = start;
            end = pre;
        }
        return dummy.next;
    }

    //反转链表
    private ListNode reverse(ListNode head) {
        ListNode pre = null;
        ListNode curr = head;
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = pre;
            pre = curr;
            curr = next;
        }
        return pre;
    }

}
```
**复杂度分析**

### 2.递归
**思路：**
反转的时候是
![](https://i.loli.net/2019/09/06/yezQiLI96BWmKMn.png)

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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode cur = head;
        int count = 0;
        while (cur != null && count != k) {
            cur = cur.next;
            count++;
        }
        if (count == k) {
            //递归从后往前
            cur = reverseKGroup(cur, k);
            //反转前 k 个
            while (count != 0) {
                count--;
                ListNode tmp = head.next;
                head.next = cur;
                cur = head;
                head = tmp;
            }
            head = cur;
        }
        return head;
    }
}
```
**复杂度分析**



---
***参考：
[powcai](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/solution/kge-yi-zu-fan-zhuan-lian-biao-by-powcai/)***
