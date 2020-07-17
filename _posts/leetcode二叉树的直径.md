---
title: 543. 二叉树的直径（Diameter of Binary Tree）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [543\. 二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

Difficulty: **简单**


给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过也可能不穿过根结点。

**示例 :**  
给定二叉树

```
          1
         / \
        2   3
       / \     
      4   5    
```

返回 **3**, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

**注意：**两结点之间的路径长度是以它们之间边的数目表示。



#### Solution

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
class Solution {
    int maxDepth = 0;
    public int diameterOfBinaryTree(TreeNode root) {
    	depth(root);
    	return maxDepth;
    }

    public int depth(TreeNode p){
    	if(p == null) return 0;
    	int leftDepth = depth(p.left);
    	int rightDepth = depth(p.right);
    	maxDepth = Math.max(leftDepth + rightDepth, maxDepth);
    	return 1 + (leftDepth > rightDepth ? leftDepth : rightDepth);
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/diameter-of-binary-tree/)***
