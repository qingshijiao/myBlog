---
title: 222.完全二叉树的节点个数（Count Complete Tree Nodes）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [222\. 完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

Difficulty: **中等**


给出一个**完全二叉树**，求出该树的节点个数。

**说明：**

的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2<sup>h</sup> 个节点。

**示例:**

```
输入:
    1
   / \
  2   3
 / \  /
4  5 6

输出: 6
```


#### Solution1 - 完全二叉树特点

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
    public int countNodes(TreeNode root) {
        if(root == null){
           return 0;
        }
        int left = countLevel(root.left);
        int right = countLevel(root.right);
        if(left == right){
            return countNodes(root.right) + (1<<left);
        }else{
            return countNodes(root.left) + (1<<right);
        }
    }
    private int countLevel(TreeNode root){
        int level = 0;
        while(root != null){
            level++;
            root = root.left;
        }
        return level;
    }
}
```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/count-complete-tree-nodes)
[xiao-ping-zi-5](https://leetcode-cn.com/problems/count-complete-tree-nodes/solution/chang-gui-jie-fa-he-ji-bai-100de-javajie-fa-by-xia/)***
