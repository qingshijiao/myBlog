---
title: 404.左叶子之和 (Sum of Left Leaves)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [404\. 左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves/)

Difficulty: **简单**


计算给定二叉树的所有左叶子之和。

**示例：**

```
    3
   / \
  9  20
    /  \
   15   7

在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24
```


#### Solution

Language: **Java**

```java
​/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
         if(root == null)
           return 0;
        if(isLeaf(root.left))
           return root.left.val + sumOfLeftLeaves(root.right);
           return sumOfLeftLeaves(root.left) + sumOfLeftLeaves(root.right);
    }
    private boolean isLeaf(TreeNode node){
        //先判定避免空指针异常
        if(node == null)
         return false;
         if(node.left == null && node.right == null)
         return true;
         return false;
}
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/sum-of-left-leaves/submissions/)***
