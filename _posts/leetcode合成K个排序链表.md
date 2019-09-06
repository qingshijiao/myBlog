---
title: 23.合并K个排序链表（Merge k Sorted Lists）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:
```
输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6
```

# 题解

## 官方题解
### 1.暴力法
**思路：**
- 遍历所有链表，将所有节点的值放到一个数组中。
- 将这个数组排序，然后遍历所有元素得到正确顺序的值。
- 用遍历得到的值，创建一个新的有序链表。

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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0){
            return null;
        }
        List<Integer> data = new ArrayList<>();
        for (ListNode listNode: lists){
            while (listNode != null){
                data.add(listNode.val);
                listNode = listNode.next;
            }
        }
        if (data.size() == 0){
            return null;
        }
        Collections.sort(data);
        ListNode head = new ListNode(data.get(0));
        ListNode p = head;
        for (int i = 1; i < data.size(); i++){
            ListNode newNode = new ListNode(data.get(i));
            p.next = newNode;
            p = newNode;
        }
        return head;
    }
}
```
**复杂度分析**
- 时间复杂度：O(NlogN),其中 NN 是节点的总数目。
  - 遍历所有的值需花费 O(N) 的时间。
  - 一个稳定的排序算法花费 O(NlogN) 的时间。
  - 遍历同时创建新的有序链表花费 O(N) 的时间。
- 空间复杂度：O(N)
  - 排序花费 O(N) 空间（这取决于你选择的算法）。
  - 创建一个新的链表花费 O(N) 的空间。
### 2.逐一比较（使用优先队列优化）
**算法：**
- 比较 k 个节点（每个链表的首节点），获得最小值的节点。
- 将选中的节点接在最终有序链表的后面。

**复杂度分析**
- 时间复杂度：O(kN) ，其中 k 是链表的数目。
  - 几乎最终有序链表中每个节点的时间开销都为 O(k) （k-1 次比较）。
  - 总共有 N 个节点在最后的链表中。
- 空间复杂度：
  - O(n) 。创建一个新的链表空间开销为 O(n) 。
  - O(1) 。重复利用原来的链表节点，每次选择节点时将它直接接在最后返回的链表后面，而不是创建一个新的节点。

### 3.逐一合并（合并二个链表 k - 1 次）
**算法：** 将合并 \text{k}k 个链表的问题转化成合并 2 个链表 \text{k-1}k-1 次。这里是 合并两个有序链表 的题目。

**复杂度分析**
- 时间复杂度：O(kN) ，其中 k 是链表的数目。
  - 我们可以在 O(n) 的时间内合并两个有序链表，其中 n 是两个链表的总长度。
  - 总共有 N 个节点在最后的链表中。
- 空间复杂度：O(1)

### 4.用优先队列优化
**算法：** 将**比较环节**用优先队列优化
**说明：** 优先队列元素不允许 null
```
public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length;
        if (len == 0) {
            return null;
        }
        PriorityQueue<ListNode> priorityQueue = new PriorityQueue<>(len, Comparator.comparingInt(a -> a.val));
        ListNode dummyNode = new ListNode(-1);
        ListNode curNode = dummyNode;
        for (ListNode list : lists) {
            if (list != null) {
                // null 不必要加入优先队列中
                priorityQueue.add(list);
            }
        }
        while (!priorityQueue.isEmpty()) {
            ListNode node = priorityQueue.poll();
            curNode.next = node;
            curNode = curNode.next;
            if (curNode.next != null) {
                priorityQueue.add(curNode.next);
            }
        }
        return dummyNode.next;
    }
```
**复杂度分析**
- 时间复杂度：O(Nlogk) ，其中 k 是链表的数目。
  - 弹出操作时，比较操作的代价会被优化到 O(log k) 。同时，找到最小值节点的时间开销仅仅为 O(1)。
  - 最后的链表中总共有 NN 个节点。
- 空间复杂度：
  - O(n) 。创造一个新的链表需要 O(n) 的开销。
  - O(k) 。以上代码采用了重复利用原有节点，所以只要 O(1) 的空间。同时优先队列（通常用堆实现）需要 O(k) 的空间（远比大多数情况的 N要小）。

### 5.分治算法
**思路：** 比逐一合并少了很多重复节点遍历
这个方法沿用了上面的解法，但是进行了较大的优化。我们不需要对大部分节点重复遍历多次。
- 将 k 个链表配对并将同一对中的链表合并。
- 第一轮合并以后， k 个链表被合并成了 k/2 个链表，平均长度为 2*N/k，然后是 k/4 个链表， k/8个链表等等。
- 重复这一过程，直到我们得到了最终的有序链表。

因此，我们在每一次配对合并的过程中都会遍历几乎全部 NN 个节点，并重复这一过程 log2(k) 次。
![](https://i.loli.net/2019/09/04/fQ4yvq3c1G5tnLZ.png)

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
    public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length;
        if (len == 0) {
            return null;
        }
        return mergeKLists(lists, 0, len - 1);
    }

    public ListNode mergeKLists(ListNode[] lists, int l, int r) {
        if (l == r) {
            return lists[l];
        }
        int mid = (r - l) / 2 + l;
        ListNode l1 = mergeKLists(lists, l, mid);
        ListNode l2 = mergeKLists(lists, mid + 1, r);
        return mergeTwoSortedListNode(l1, l2);
    }

    private ListNode mergeTwoSortedListNode(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        }
        if (l2 == null) {
            return l1;
        }
        if (l1.val < l2.val) {
            l1.next = mergeTwoSortedListNode(l1.next, l2);
            return l1;
        }
        l2.next = mergeTwoSortedListNode(l1, l2.next);
        return l2;
    }
}
```
**复杂度分析**
![](https://i.loli.net/2019/09/04/6uHINfscgwkzyqM.png)


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/merge-k-sorted-lists/solution/he-bing-kge-pai-xu-lian-biao-by-leetcode/)***
