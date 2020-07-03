---
title: 515. 在每个树行中找最大值 (Find Largest Value in Each Tree Row)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [515\. 在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)

Difficulty: **中等**


您需要在二叉树的每一行中找到最大的值。

**示例：**

```
输入: 

          1
         / \
        3   2
       / \   \  
      5   3   9 

输出: [1, 3, 9]
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
    public List<Integer> largestValues(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        if (root == null)
            return res;
        helper(root, 0,res);
        return res;
    }

    private void helper(TreeNode node, int level, List<Integer> res) {
        if (node == null)
            return ;
        if (level == res.size())
            res.add(node.val);
        else
            res.set(level, Math.max(res.get(level), node.val));
        helper(node.left, level + 1, res);
        helper(node.right, level + 1, res);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)***
