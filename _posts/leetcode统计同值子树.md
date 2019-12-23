---
title: 250.移位字符串分组（Displacement tandem grouping）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

Given a binary tree, count the number of uni-value subtrees.

A Uni-value subtree means all nodes of the subtree have the same value.

For example:
Given binary tree,
```
    5
   / \
  1   5
 / \   \
5   5   5
```

#### Solution - 递归

Language: **Java**

```java


/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    private int count;
    private boolean unival(TreeNode root) {
        boolean uni = true;
        if (root.left != null) uni &= unival(root.left) && root.val == root.left.val;
        if (root.right != null) uni &= unival(root.right) && root.val == root.right.val;
        if (uni) count ++;
        return uni;
    }
    public int countUnivalSubtrees(TreeNode root) {
        if (root == null) return 0;
        unival(root);
        return count;
    }


```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/count-univalue-subtrees/)
[jmspan](https://blog.csdn.net/jmspan/article/details/51085304)***
