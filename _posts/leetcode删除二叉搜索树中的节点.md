---
title: 450. 删除二叉搜索树中的节点（Delete Node in a BST）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [450\. 删除二叉搜索树中的节点](https://leetcode-cn.com/problems/delete-node-in-a-bst/)

Difficulty: **中等**


给定一个二叉搜索树的根节点 **root** 和一个值 **key**，删除二叉搜索树中的 **key **对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

1.  首先找到需要删除的节点；
2.  如果找到了，删除它。

**说明：** 要求算法时间复杂度为 O(h)，h 为树的高度。

**示例:**

```
root = [5,3,6,2,4,null,7]
key = 3

    5
   / \
  3   6
 / \   \
2   4   7

给定需要删除的节点值是 3，所以我们首先找到 3 这个节点，然后删除它。

一个正确的答案是 [5,4,6,2,null,null,7], 如下图所示。

    5
   / \
  4   6
 /     \
2       7

另一个正确答案是 [5,2,6,null,4,null,7]。

    5
   / \
  2   6
   \   \
    4   7
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
public class Pair <A, B> {
    public final A fst;
    public final B snd;

    public Pair(A a, B b) {
        fst = a; 
        snd = b;
    }  
}

class Solution {
     public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        if (root.val == key && root.right == null) {
            return root.left;
        } else {
            return helper(root, key);
        }
    }

    private TreeNode helper(TreeNode root, int key) {
        if (root == null) {
            return null;
        }
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
            return root;
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
            return root;
        } else {
            Pair<TreeNode, TreeNode> nodePair = removeMin(root.right);
            if (nodePair.fst != null) {
                nodePair.fst.right = nodePair.snd;
                nodePair.fst.left = root.left;
            }
            return nodePair.fst;
        }
    }


    /**
     * 删除最小的节点
     *
     * @return <最小结点，删除之后的根节点>
     */
    private Pair<TreeNode, TreeNode> removeMin(TreeNode root) {
        if (root == null) {
            return new Pair<>(null, null);
        }
        TreeNode dummyNode = new TreeNode(0);
        dummyNode.left = root;

        TreeNode parentNode = dummyNode;
        TreeNode minNode = root;
        while (minNode.left != null) {
            parentNode = minNode;
            minNode = minNode.left;
        }
        parentNode.left = minNode.right;
        return new Pair<>(minNode, dummyNode.left);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/delete-node-in-a-bst/)***
