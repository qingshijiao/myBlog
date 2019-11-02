---
title: 148.排序链表（Sort List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

示例 1:
```
输入: 4->2->1->3
输出: 1->2->3->4
```
示例 2:
```
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.归并排序 - 递归
**思路：**
![](https://pic.leetcode-cn.com/8c47e58b6247676f3ef14e617a4686bc258cc573e36fcf67c1b0712fa7ed1699-Picture2.png)

```
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null)
            return head;
        ListNode fast = head.next, slow = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        ListNode tmp = slow.next;
        slow.next = null;
        ListNode left = sortList(head);
        ListNode right = sortList(tmp);
        ListNode h = new ListNode(0);
        ListNode res = h;
        while (left != null && right != null) {
            if (left.val < right.val) {
                h.next = left;
                left = left.next;
            } else {
                h.next = right;
                right = right.next;
            }
            h = h.next;
        }
        h.next = left != null ? left : right;
        return res.next;
    }
}

```

### 2.归并排序 - 从底至顶直接合并
**思路：**
![](https://pic.leetcode-cn.com/c1d5347aa56648afdec22372ee0ed13cf4c25347bd2bb9727b09327ce04360c2-Picture1.png)

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

    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        // 这里设置 64 ，是一个绰绰有余的数字，可以满足结点数量为 2^64 这么多的单链表的排序
        ListNode[] counter = new ListNode[64];
        ListNode curNode = head;
        // 遍历到的最大的 counter 数组的索引
        int maxIndex = 0;
        while (curNode != null) {
            // 先把当前元素暂存起来，马上我们就要把它放到 counter 数组合适的位置上
            ListNode carryNode = curNode;
            // curNode 指针马上后移，方便下次处理
            curNode = curNode.next;
            // 拿出的节点就和原来的链表没有关系了，我们在 counter 数组中完成排序，所以要切断它和原链表的关系
            carryNode.next = null;
            // 尝试从 counter 数组 0 号索引开始放置
            int i = 0;
            // 只要非空当前位置非空，就进行一次 merge，merge 以后尝试放到下一格，如果下一格非空就继续合并
            // 合并以后再尝试放到下一格，直到下一格为空，直接放在那个为空的下一格就好
            while (counter[i] != null) {
                ListNode newMergeNode = mergeOfTwoSortedListNode(carryNode, counter[i]);
                counter[i] = null;
                i++;
                carryNode = newMergeNode;
            }
            // 遇到了空，就把 carryNode 放在数组的这个位置上
            counter[i] = carryNode;
            // 记录最多使用到 counter 数组的第几位，最后合并的时候要用上
            if (i > maxIndex) {
                maxIndex = i;
            }
        }
        // 遍历整个 count 数组，将它们全部归并，这个操作就和归并 n 个有序单链表是一样的了，我们这里采用两两归并
        // 还可以采用 LeetCode 第 23 题的办法完成这一步
        // 参考：https://liweiwei1419.github.io/leetcode-solution/leetcode-0023-merge-k-sorted-lists/
        ListNode res = null;
        for (int i = 0; i <= maxIndex; i++) {
            if (counter[i] != null) {
                res = mergeOfTwoSortedListNode(res, counter[i]);
            }
        }
        return res;
    }

    /**
     * 归并两个已经排好序的单链表，是我们非常熟悉的操作了，可以递归完成，也可以穿针引线，这里我们递归完成
     *
     * @param l1 顺序存放的单链表1
     * @param l2 顺序存放的单链表2
     * @return 合并以后的单链表
     */
    private ListNode mergeOfTwoSortedListNode(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        if (l1.val < l2.val) {
            l1.next = mergeOfTwoSortedListNode(l1.next, l2);
            return l1;
        } else {
            l2.next = mergeOfTwoSortedListNode(l1, l2.next);
            return l2;
        }
    }

}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/lru-cache/solution/lru-huan-cun-ji-zhi-by-leetcode/)
[jyd](https://leetcode-cn.com/problems/sort-list/solution/sort-list-gui-bing-pai-xu-lian-biao-by-jyd/)***
