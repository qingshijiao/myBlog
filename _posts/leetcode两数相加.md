---
title: 2.两数相加(Add Two Numbers)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

> 输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
>
>输出：7 -> 0 -> 8
>
>原因：342 + 465 = 807


# 题解

## 官方题解
### 1.初等数学
**思想**：和我们笔算加法一样，要考虑到进位carry，*相加时缺位补0*
测试用例|说明
---|:--:|---:
l1=[0,1]，l2=[0,1,2]|当一个列表比另一个列表长时
l1=[]，l2=[0,1]|当一个列表为空时，即出现空列表
l1=[9,9]，l2=[1]|求和运算最后可能出现额外的进位，这一点很容易被遗忘

```
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    //先创建一个初始节点
    ListNode dummyHead = new ListNode(0);
    ListNode p = l1, q = l2, curr = dummyHead;
    //进位
    int carry = 0;
    while (p != null || q != null) {
        //由于两数的位数可能不同，我们把缺位补0
        int x = (p != null) ? p.val : 0;
        int y = (q != null) ? q.val : 0;
        int sum = carry + x + y;
        carry = sum / 10;
        curr.next = new ListNode(sum % 10);
        curr = curr.next;
        //当出现缺位时，假设p比q多两位，这时每次循环p会向后移动，q不移动，
        //由于q一直指向null，会补为0，避免了空指针后移
        if (p != null) p = p.next;
        if (q != null) q = q.next;
    }
    if (carry > 0) {
        curr.next = new ListNode(carry);
    }
    return dummyHead.next;
}
```

> 复杂度分析
>
> - 时间复杂度：O(max(m, n))，假设 mm 和 nn 分别表示 l1l1 和 l2l2 的长度，上面的算法最多重复 \max(m, n)次
> - 空间复杂度：O(max(m, n)), 新列表的长度最多为max(m,n)+1。

## 其他题解
### 1.
**思想：** 整体思路都差不多, 加减的结果直接放在l1, 节省了内存

```
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode p = l1;
        ListNode q = l2;
        int addNum = 0;
        //只需判断一条链为空就行，循环中.next保证了两条链只有计算完成才会同时进入空。
        while(q!=null){
            //其中一条链为空，缺位补0结点，仍可计算
            if(p.next==null && q.next!=null)
                p.next = new ListNode(0);
            if(q.next==null && p.next!=null)
                q.next = new ListNode(0);
            int sumAll = addNum + p.val + q.val;
            p.val = sumAll % 10;
            addNum = sumAll / 10;
            //进位
            if(p.next == null && q.next == null && addNum!=0)
                p.next = new ListNode(addNum);
            p = p.next;
            q = q.next;
        }
        return l1;
    }
```

---
***参考：[领扣](https://leetcode-cn.com/problems/add-two-numbers/solution/liang-shu-xiang-jia-by-leetcode/)***
