---
title: 143.重排链表（Reorder List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个单链表 L：L0→L1→…→Ln-1→Ln ，
将其重新排列后变为： L0→Ln→L1→Ln-1→L2→Ln-2→…

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例 1:
```
给定链表 1->2->3->4, 重新排列为 1->4->2->3.
```
示例 2:
```
给定链表 1->2->3->4->5, 重新排列为 1->5->2->4->3.
```


# 题解

## 官方题解
暂无

## 其他题解
### 1.存储
**思路：** 使用线性表存储每个节点。

```
public void reorderList(ListNode head) {
    if (head == null) {
        return;
    }
    //存到 list 中去
    List<ListNode> list = new ArrayList<>();
    while (head != null) {
        list.add(head);
        head = head.next;
    }
    //头尾指针依次取元素
    int i = 0, j = list.size() - 1;
    while (i < j) {
        list.get(i).next = list.get(j);
        i++;
        //偶数个节点的情况，会提前相遇
        if (i == j) {
            break;
        }
        list.get(j).next = list.get(i);
        j--;
    }
    list.get(i).next = null;
}

```

### 2.递归
**思路：**

![](https://pic.leetcode-cn.com/cc05523815b2eb5baf80741809193cc5b17f29b6a6efe2c235007a036aff5625.jpg)
![](https://pic.leetcode-cn.com/0a9173afb9b7f62587f5132689ad5bceb98cd24f8f7a3d5f938ca2886d308892.jpg)

```
public void reorderList(ListNode head) {

    if (head == null || head.next == null || head.next.next == null) {
        return;
    }
    int len = 0;
    ListNode h = head;
    //求出节点数
    while (h != null) {
        len++;
        h = h.next;
    }

    reorderListHelper(head, len);
}

private ListNode reorderListHelper(ListNode head, int len) {
    if (len == 1) {
        ListNode outTail = head.next;
        head.next = null;
        return outTail;
    }
    if (len == 2) {
        ListNode outTail = head.next.next;
        head.next.next = null;
        return outTail;
    }
    //得到对应的尾节点，并且将头结点和尾节点之间的链表通过递归处理
    ListNode tail = reorderListHelper(head.next, len - 2);
    ListNode subHead = head.next;//中间链表的头结点
    head.next = tail;
    ListNode outTail = tail.next;  //上一层 head 对应的 tail
    tail.next = subHead;
    return outTail;
}

```

### 3.题意
**思路：**
主要是三步，举个例子。
```
1 -> 2 -> 3 -> 4 -> 5 -> 6
第一步，将链表平均分成两半，使用快慢指针
1 -> 2 -> 3
4 -> 5 -> 6

第二步，将第二个链表逆序
1 -> 2 -> 3
6 -> 5 -> 4

第三步，依次连接两个链表
1 -> 6 -> 2 -> 5 -> 3 -> 4

```

```
public void reorderList(ListNode head) {
    if (head == null || head.next == null || head.next.next == null) {
        return;
    }
    //找中点，链表分成两个
    ListNode slow = head;
    ListNode fast = head;
    while (fast.next != null && fast.next.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    ListNode newHead = slow.next;
    slow.next = null;

    //第二个链表倒置
    newHead = reverseList(newHead);

    //链表节点依次连接
    while (newHead != null) {
        ListNode temp = newHead.next;
        newHead.next = head.next;
        head.next = newHead;
        head = newHead.next;
        newHead = temp;
    }

}

private ListNode reverseList(ListNode head) {
    if (head == null) {
        return null;
    }
    ListNode tail = head;
    head = head.next;

    tail.next = null;

    while (head != null) {
        ListNode temp = head.next;
        head.next = tail;
        tail = head;
        head = temp;
    }

    return tail;
}


```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/reorder-list/submissions/)
[windliang](https://leetcode-cn.com/problems/reorder-list/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-34/)***
