---
title: 333.最大 BST 子树 (Largest BST Subtree)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目描述:
给定一个二叉树，找到其中最大的二叉搜索树（BST）子树，其中最大指的是子树节点数最多的。

注意:

子树必须包含其所有后代。

示例:
示例:

输入: [10,5,15,1,8,null,7]

   10
   / \
  5  15
 / \   \
1   8   7

输出: 3
解释: 高亮部分为最大的 BST 子树。
     返回值 3 在这个样例中为子树大小。
进阶:

你能想出用 O(n) 的时间复杂度解决这个问题吗？


#### Solution

Language: **python**

```python
​# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def largestBSTSubtree(self, root: TreeNode) -> int:

        def helper(root):
            if not root:
                return float("inf"), float("-inf"), 0
            l_min, l_max, lv = helper(root.left)
            r_min, r_max, rv = helper(root.right)
            # print(root.val, l_max, r_min)
            if  l_max < root.val < r_min:
                return min(l_min, root.val), max(root.val, r_max), 1 + lv + rv
            return float("-inf"), float("inf"), max(lv, rv)

        return helper(root)[2]
```

---
***参考:
[p](https://zhuanlan.zhihu.com/p/92129981)***
