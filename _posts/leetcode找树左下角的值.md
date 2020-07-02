---
title: 513. 找树左下角的值 (Find Bottom Left Tree Value)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [513\. 找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)

Difficulty: **中等**


给定一个二叉树，在树的最后一行找到最左边的值。

**示例 1:**

```
输入:

    2
   / \
  1   3

输出:
1
```

**示例 2:**

```
输入:

        1
       / \
      2   3
     /   / \
    4   5   6
       /
      7

输出:
7
```

**注意:** 您可以假设树（即给定的根节点）不为 **NULL**。


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
    int res = 0;
    int height = 0;//记录当前的高度
    public int findBottomLeftValue(TreeNode root) {
        if (root == null) return -1;
        helper(root ,1);//1就是depth
        return res;
    }
    public void helper(TreeNode root, int depth) {
        if (root == null) return;
        if (height < depth) {//没找到最下面就继续找
            res = root.val;
            height = depth;
        }
        helper(root.left, depth + 1);
        helper(root.right, depth + 1);
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)***
