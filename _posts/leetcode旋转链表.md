---
title: 61. 旋转链表（Rotate List）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个链表，旋转链表，将链表每个节点向右移动 k 个位置，其中 k 是非负数。

示例 1:
```
输入: 1->2->3->4->5->NULL, k = 2
输出: 4->5->1->2->3->NULL
解释:
向右旋转 1 步: 5->1->2->3->4->NULL
向右旋转 2 步: 4->5->1->2->3->NULL
```
示例 2:
```
输入: 0->1->2->NULL, k = 4
输出: 2->0->1->NULL
解释:
向右旋转 1 步: 2->0->1->NULL
向右旋转 2 步: 1->2->0->NULL
向右旋转 3 步: 0->1->2->NULL
向右旋转 4 步: 2->0->1->NULL
```



# 题解

## 官方题解
### 1.链表成环再断开
**思路：** 链表中的点已经相连，一次旋转操作意味着：

- 先将链表闭合成环
- 找到相应的位置断开这个环，确定新的链表头和链表尾

![](https://pic.leetcode-cn.com/e3371c6b03e3c8d3758dcf0b35a45d0a6b39c111373cf7b5bde53e14b6271a04-61.png)
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
  public List<List<String>> solveNQueens(int n) {
        int[] col=new int[n];//棋子放置位置
        int[] row=new int[n];
        int[] dig=new int[2*n-1];
        int[] hill=new int[2*n-1];
        List<List<String>> answer=new ArrayList<>();
        List<List<String>> a=place(n,0,row,dig,hill,col,answer);
        return a;

    }
    List<List<String>>  place (int n,int m,int[]row,int[]dig,int [] hill,int[] col,List<List<String>> answer){
        if(n==m) {
            List<String> ans=new ArrayList<String>();

            for (int i=0;i<n;i++){
                StringBuilder sol=new StringBuilder();
                for(int j=0;j<col[i];j++){
                    sol.append('.');
                }
                sol.append('Q');
                for(int j=(col[i]+1);j<n;j++){
                    sol.append('.');
                }
                String solu=sol.toString();
                ans.add(solu);
            }
            answer.add(ans);
        }
        else{
            for(int i=0;i<n;i++) {
                int res=row[i]+dig[i+m]+hill[i-m+n-1];
                if(res==0){
                    col[m]=i;
                    row[i]=1;
                    dig[i+m]=1;
                    hill[i-m+n-1]=1;
                    place(n,(m+1),row,dig,hill,col,answer);
                    col[m]=0;
                    row[i]=0;
                    dig[i+m]=0;
                    hill[i-m+n-1]=0;
                }

            }
        }
        return answer;

    }

}


```

## 其他题解
### 1.计算链表的长度
**思路：**
1. 求出链表的长度len
2. k = k%len取余就是我们要右移的距离。
3. 找到倒数第k个位置。可以使用双指针法。
4. 记录慢指针的next节点，这就是最后要返回的节点。


![](https://pic.leetcode-cn.com/08afd991d5aa8171c3daa0edf0c4e3dd46094d94e34e114f47f01b6b01d50f38-%E5%9B%BE%E7%89%87.png)
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
    public ListNode rotateRight(ListNode head, int k) {
        if (head == null || k == 0) {
            return head;
        }
        ListNode tmp = head;
        int len = 0;
        //求出链表的长度
        while (tmp != null) {
            tmp = tmp.next;
            len++;
        }
        k = k % len;  //以len为一个周期
        if (k == 0) {
            return head;
        }
        //保存一下头节点
        ListNode node = head;
        //快慢指针
        tmp = head;
        while (k > 0) {
            k--;
            tmp = tmp.next;
        }
        while (tmp.next != null) {
            head = head.next;
            tmp = tmp.next;
        }
        //记录next的位置，也就是返回值的头结点
        ListNode res = head.next;
        //断开连接
        head.next = null;
        //后一段的末尾指向前一段的开头
        tmp.next = node;
        return res;

    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/rotate-list/solution/xuan-zhuan-lian-biao-by-leetcode/)
[reedfan](https://leetcode-cn.com/problems/rotate-list/solution/ji-bai-liao-91de-javayong-hu-qing-xi-yi-dong-by-re/)***
