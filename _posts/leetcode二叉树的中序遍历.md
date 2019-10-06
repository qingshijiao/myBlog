---
title: 94.二叉树的中序遍历（Binary Tree Inorder Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树，返回它的中序 遍历。

示例:
```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？


# 题解

## 官方题解
### 1.递归
**思路：**

```
class Solution {
    public List < Integer > inorderTraversal(TreeNode root) {
        List < Integer > res = new ArrayList < > ();
        helper(root, res);
        return res;
    }

    public void helper(TreeNode root, List < Integer > res) {
        if (root != null) {
            if (root.left != null) {
                helper(root.left, res);
            }
            res.add(root.val);
            if (root.right != null) {
                helper(root.right, res);
            }
        }
    }
}

```
**复杂度分析：**
- 时间复杂度： O(n)。递归函数 T(n)=2⋅T(n/2)+1。
- 空间复杂度：最坏情况下需要空间O(n)，平均情况为O(logn)。


### 2.基于栈的遍历
**思路：**
![](https://pic.leetcode-cn.com/45b974ac01bb9e32983a9650f2fd94eb7c0cb85747d9a01c6921e3070b4d9999-image.png)

```
public class Solution {
    public List < Integer > inorderTraversal(TreeNode root) {
        List < Integer > res = new ArrayList < > ();
        Stack < TreeNode > stack = new Stack < > ();
        TreeNode curr = root;
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            res.add(curr.val);
            curr = curr.right;
        }
        return res;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)。
- 空间复杂度：O(n)。

### 3.莫里斯遍历
**思路：** 本方法中，我们使用一种新的数据结构：线索二叉树。方法如下：

![](https://i.loli.net/2019/10/06/rICMsVWcPp9tw84.png)

```
class Solution {
    public List < Integer > inorderTraversal(TreeNode root) {
        List < Integer > res = new ArrayList < > ();
        TreeNode curr = root;
        TreeNode pre;
        while (curr != null) {
            if (curr.left == null) {
                res.add(curr.val);
                curr = curr.right; // move to next right node
            } else { // has a left subtree
                pre = curr.left;
                while (pre.right != null) { // find rightmost
                    pre = pre.right;
                }
                pre.right = curr; // put cur after the pre node
                TreeNode temp = curr; // store cur node
                curr = curr.left; // move cur to the top of the new tree
                temp.left = null; // original cur left be null, avoid infinite loops
            }
        }
        return res;
    }
}

```
**复杂度分析：**
- 时间复杂度：O(n)。 想要证明时间复杂度是O(n)，最大的问题是找到每个节点的前驱节点的时间复杂度。乍一想，找到每个节点的前驱节点的时间复杂度应该是 O(nlogn)，因为找到一个节点的前驱节点和树的高度有关。
但事实上，找到所有节点的前驱节点只需要 O(n) 时间。一棵 n 个节点的二叉树只有 n-1n−1 条边，每条边只可能使用2次，一次是定位节点，一次是找前驱节点。
故复杂度为 O(n)。
- 空间复杂度：O(n)。使用了长度为 n 的数组。


## 其他题解
暂无


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/solution/er-cha-shu-de-zhong-xu-bian-li-by-leetcode/)***
