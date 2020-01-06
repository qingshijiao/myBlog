---
title: 272.最近的二分搜索树的值之二（Closest Binary Search Tree Value II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
272.Closest Binary Search Tree Value II
Given a non-empty binary search tree and a target value, find k values in the BST that are closest to the target.

Note:

- Given target value is a floating point.
- You may assume k is always valid, that is: k ≤ total nodes.
- You are guaranteed to have only one unique set of k values in the BST that are closest to the target.


Example:
```
Input: root = [4,2,5,1,3], target = 3.714286, and k = 2

    4
   / \
  2   5
 / \
1   3

Output: [4,3]
```

**Follow up:**
Assume that the BST is balanced, could you solve it in less than O(n) runtime (where n = total nodes)?


#### Solution

还是使用inorder traversal来遍历树，同时维护一个size为k的LinkedList或者Deque。这个原理类似于sliding window。

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
    public List<Integer> closestKValues(TreeNode root, double target, int k) {
        LinkedList<Integer> res = new LinkedList<>();
        inOrderTraversal(root, target, k, res);
        return res;
    }

    private void inOrderTraversal(TreeNode root, double target, int k, LinkedList<Integer> res) {
        if (root == null) {
            return;
        }
        inOrderTraversal(root.left, target, k, res);
        if (res.size() < k) {
            res.add(root.val);
        } else if(res.size() == k) {
            if (Math.abs(res.getFirst() - target) > (Math.abs(root.val - target))) {
                res.removeFirst();
                res.addLast(root.val);
            } else {
                return;
            }
        }
        inOrderTraversal(root.right, target, k, res);
    }
}
```


---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5031304.html)***
