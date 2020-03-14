---
title: 298.二叉树最长连续序列(Binary Tree Longest Consecutive Sequence)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given a binary tree, find the length of the longest consecutive sequence path.



The path refers to any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The longest consecutive path need to be from parent to child (cannot be the reverse).

For example,
```
   1
    \
     3
    / \
   2   4
        \
         5
```
Longest consecutive sequence path is 3-4-5, so return 3.
```
   2
    \
     3
    /
   2
  /
 1
```
Longest consecutive sequence path is 2-3,not3-2-1, so return 2.


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
public class Solution {
    private int maxLen = 0;

    public int longestConsecutive(TreeNode root) {
        longestConsecutive(root, 0, 0);
        return maxLen;
    }

    private void longestConsecutive(TreeNode root, int lastVal, int curLen) {
        if (root == null) return;
        if (root.val != lastVal + 1) curLen = 1;
        else curLen++;
        maxLen = Math.max(maxLen, curLen);
        longestConsecutive(root.left, root.val, curLen);
        longestConsecutive(root.right, root.val, curLen);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-tree-longest-consecutive-sequence/)
[lightwindy](https://www.cnblogs.com/lightwindy/p/8692384.html)***
