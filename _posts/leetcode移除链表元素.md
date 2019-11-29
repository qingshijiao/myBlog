---
title: 203.移除链表元素（Remove Linked List Elements）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [203\. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)

Difficulty: **简单**


删除链表中等于给定值 **_val _**的所有节点。

**示例:**

```
输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
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
    public ListNode removeElements(ListNode head, int val) {
        //创建一个虚拟头结点
        ListNode dummyNode=new ListNode(val-1);
        dummyNode.next=head;
        ListNode prev=dummyNode;
        //确保当前结点后还有结点
        while(prev.next!=null){
            if(prev.next.val==val){
                prev.next=prev.next.next;
            }else{
                prev=prev.next;
            }
        }
        return dummyNode.next;
    }
}
```
---
***参考：
[LeetCode](https://leetcode-cn.com/problems/remove-linked-list-elements/submissions/)
[lewis](https://leetcode-cn.com/problems/remove-linked-list-elements/solution/203yi-chu-lian-biao-yuan-su-by-lewis-dxstabdzew/)***
