---
title: 19.删除链表的倒数第N个节点（Remove Nth Node From End of List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：
> 给定一个链表: 1->2->3->4->5, 和 n = 2.
> 当删除了倒数第二个节点后，链表变为 1->2->3->5.

**说明：**
给定的 n 保证是有效的。

**进阶：**
你能尝试使用一趟扫描实现吗？


# 题解

## 官方题解
### 1.两遍遍历
**思路：** 我们注意到这个问题可以容易地简化成另一个问题：删除从列表开头数起的第 (L - n + 1) 个结点，其中 L 是列表的长度。只要我们找到列表的长度 L，这个问题就很容易解决。
**算法：** 首先我们将添加一个哑结点作为辅助，该结点位于列表头部。哑结点用来简化某些极端情况，例如列表中只含有一个结点，或需要删除列表的头部。
![](https://pic.leetcode-cn.com/a476f4e932fa4499e22902dcb18edba41feaf9cfe4f17869a90874fbb1fd17f5-file_1555694537876)

```
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    int length  = 0;
    ListNode first = head;
    while (first != null) {
        length++;
        first = first.next;
    }
    length -= n;
    first = dummy;
    while (length > 0) {
        length--;
        first = first.next;
    }
    first.next = first.next.next;
    return dummy.next;
}
```
**复杂度分析：**
- 时间复杂度：O(L)，该算法对列表进行了两次遍历，首先计算了列表的长度 L 其次找到第 (L - n) 个结点。 操作执行了 2L-n 步，时间复杂度为 O(L)。
- 空间复杂度：O(1)，我们只用了常量级的额外空间。


### 2.双指针
**思路：** 使用两个指针，间隔为 N。当前一个指针遍历到末尾时，后一个指针刚好遍历到倒数第 N 个节点的前一个节点。
**算法：**上述算法可以优化为只使用一次遍历。我们可以使用两个指针而不是一个指针。第一个指针从列表的开头向前移动 n+1 步，而第二个指针将从列表的开头出发。现在，这两个指针被 n 个结点分开。我们通过同时移动两个指针向前来保持这个恒定的间隔，直到第一个指针到达最后一个结点。此时第二个指针将指向从最后一个结点数起的第 n 个结点。我们重新链接第二个指针所引用的结点的 next 指针指向该结点的下下个结点。
![](https://pic.leetcode-cn.com/4e134986ba59f69042b2769b84e3f2682f6745033af7bcabcab42922a58091ba-file_1555694482088)
```
public ListNode removeNthFromEnd(ListNode head, int n) {
    ListNode dummy = new ListNode(0);
    dummy.next = head;
    ListNode first = dummy;
    ListNode second = dummy;
    // Advances first pointer so that the gap between first and second is n nodes apart
    for (int i = 1; i <= n + 1; i++) {
        first = first.next;
    }
    // Move first to the end, maintaining the gap
    while (first != null) {
        first = first.next;
        second = second.next;
    }
    second.next = second.next.next;
    return dummy.next;
}
```
**复杂度分析：**
- 时间复杂度：O(L)，该算法对含有 L 个结点的列表进行了一次遍历。因此时间复杂度为 O(L)。
- 空间复杂度：O(1)，我们只用了常量级的额外空间。

## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/two-sum/solution/shan-chu-lian-biao-de-dao-shu-di-nge-jie-dian-by-l/)***
