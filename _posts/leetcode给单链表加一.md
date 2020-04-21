---
title: 369.给单链表加一

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
用一个 非空 单链表表示一个非负整数，将这个整数加一。

你可以假设这个整数除了 0 本身，没有任何前导 0 。

这个整数的各个数位按照高位在链表头，低位在链表尾的顺序排列。

示例:

输入: [1,2,3]
输出: [1,2,4]


#### Solution

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
    public ListNode plusOne(ListNode head) {
        ListNode newHead = new ListNode(0);
        newHead.next = head;
        ListNode curr = newHead;
        ListNode curr_head = newHead;
        while(curr.next!=null){
            curr = curr.next;
            if(curr.val != 9){
                curr_head = curr;
            }
        }
        if(curr_head == curr){
            curr.val++;
        }else{
            curr_head.val++;
            curr = curr_head;
            while(curr.next != null){
                curr = curr.next;
                curr.val = 0;
            }
        }
        if(newHead.val == 0){
            newHead.next = null;
            return head;
        }else{
            return newHead;
        }

    }
}

```
---
***参考:
[weixin_39784818](https://blog.csdn.net/weixin_39784818/article/details/93707981)***
