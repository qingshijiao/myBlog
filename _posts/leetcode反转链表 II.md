---
title: 92. 反转链表 II（Reverse Linked List II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。

**说明:**
1 ≤ m ≤ n ≤ 链表长度。

示例:
```
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```


# 题解

## 官方题解
### 1.递归
**思路：**
下面是一系列整个算法的示意图，希望能够帮助你理解清楚。

![](http://pic.leetcode-cn.com/1adc7164bea5cd650af1545682900c792bd37a82df607aeb4f87a233d3eb69cf-image.png)

这是递归过程的第一步。给定所用链表，left 和 right 指针从链表的 head 开始。第一步是以更新过的 m 和 n 进行递归调用，换而言之，它们的值各自减 1。此外，left 和 right 指针向前移动一位。

![](https://pic.leetcode-cn.com/162f18666a30ffd98e185da1311f2daa48b087b03d3a9eefeeb9541eafbcd013-image.png)

接下来的两步展示了 left 和 right 指针在链表中的移动。注意到在第二步之后，left 指针抵达了目标位置。因此，后续不再移动。从现在起，只有 right 指针继续移动，直到抵达结点 6。

![](https://pic.leetcode-cn.com/4213450e7d9466ddf22f289d5e753df47a94a9a87789312a02de2979ed161718-image.png)

如你所见，在第五步之后，两个指针均抵达了目标位置，可以开始进行回溯。我们不再继续递归。回溯过程中的操作是交换 left 和 right 结点的数据。

![](https://pic.leetcode-cn.com/36b2ed0c1859c5574a17597070797d8f26b77a9c13a0c3462ea150b1058fbbce-image.png)

如你所见，在第三步（回溯）之后，right 指针 穿过了 left 指针，此时已经完成了要求部分链表的反转。结果是 [7 → 9 → 8 → 1 → 10 → 2 → 6]。 于是不再进行数据交换，在代码中，我们使用全局 boolean 变量 flag 来停止数据交换。不能直接跳出递归。



```
class Solution {

    // Object level variables since we need the changes
    // to persist across recursive calls and Java is pass by value.
    private boolean stop;
    private ListNode left;

    public void recurseAndReverse(ListNode right, int m, int n) {

        // base case. Don't proceed any further
        if (n == 1) {
            return;
        }

        // Keep moving the right pointer one step forward until (n == 1)
        right = right.next;

        // Keep moving left pointer to the right until we reach the proper node
        // from where the reversal is to start.
        if (m > 1) {
            this.left = this.left.next;
        }

        // Recurse with m and n reduced.
        this.recurseAndReverse(right, m - 1, n - 1);

        // In case both the pointers cross each other or become equal, we
        // stop i.e. don't swap data any further. We are done reversing at this
        // point.
        if (this.left == right || right.next == this.left) {
            this.stop = true;
        }

        // Until the boolean stop is false, swap data between the two pointers
        if (!this.stop) {
            int t = this.left.val;
            this.left.val = right.val;
            right.val = t;

            // Move left one step to the right.
            // The right pointer moves one step back via backtracking.
            this.left = this.left.next;
        }
    }

    public ListNode reverseBetween(ListNode head, int m, int n) {
        this.left = head;
        this.stop = false;
        this.recurseAndReverse(head, m, n);
        return head;
    }
}
```
**复杂度分析：**
- 时间复杂度： O(N)。对每个结点最多处理两次。递归过程回溯。在回溯过程中，我们只交换了一半的结点，但总复杂度是 O(N)。
- 空间复杂度：最坏情况下为 O(N)。在最坏的情况下，我们需要反转整个链表。这是此时递归栈的大小。

### 2.迭代链接反转
**思路：**
在上个方法中，我们研究了一种反转给定链表部分的算法，该算法不改变给定链表的内在结构，只是修改了对于结点的值。 然而，有时可能无法修改结点的数据值。这时，我们就需要改变结点的链接来完成反转。

从位置 m 到位置 n 的全部结点，我们需要反转每个结点的 next 指针。下面来看看具体的算法。


![](https://pic.leetcode-cn.com/bf38eaeb92184fbfb55bd76336c7f746b6f01b3c83bd921268afe84a3c3cf183-image.png)

![](https://pic.leetcode-cn.com/08d4eb39be0db6ded442a208399b5778bbab1cf75c26bc5b3d93128b7c224cb4-image.png)

![](https://pic.leetcode-cn.com/77af1e2ca8bd5f9ccc89802094ce07e2505c6b4483ccd6887f2762a6e67310e1-image.png)

![](https://pic.leetcode-cn.com/f634c434bcc5092d84b3125a4cd7c723aa3ddd53dcfb9ec3077423cbff1d2f85-image.png)


![](https://pic.leetcode-cn.com/b11861e6d3a86cdec19152d442dd243aaf0fb6c914787e7cf60990f2ecf0d558-image.png)

![](https://pic.leetcode-cn.com/968684e83b4cbc4b4db6f80e3bda03748729af672e702a8d3473b24cd04a7092-image.png)




```
class Solution {
    public ListNode reverseBetween(ListNode head, int m, int n) {

        // Empty list
        if (head == null) {
            return null;
        }

        // Move the two pointers until they reach the proper starting point
        // in the list.
        ListNode cur = head, prev = null;
        while (m > 1) {
            prev = cur;
            cur = cur.next;
            m--;
            n--;
        }

        // The two pointers that will fix the final connections.
        ListNode con = prev, tail = cur;

        // Iteratively reverse the nodes until n becomes 0.
        ListNode third = null;
        while (n > 0) {
            third = cur.next;
            cur.next = prev;
            prev = cur;
            cur = third;
            n--;
        }

        // Adjust the final connections as explained in the algorithm
        if (con != null) {
            con.next = prev;
        } else {
            head = prev;
        }

        tail.next = cur;
        return head;
    }
}
```
**复杂度分析：**
- 时间复杂度：  O(N)。考虑包含 NN 个结点的链表。对每个节点最多会处理（第 nn 个结点之后的结点不处理）。
- 空间复杂度： O(1)。我们仅仅在原有链表的基础上调整了一些指针，只使用了 O(1) 的额外存储空间来获得结果。


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/reverse-linked-list-ii/solution/fan-zhuan-lian-biao-ii-by-leetcode/)***
