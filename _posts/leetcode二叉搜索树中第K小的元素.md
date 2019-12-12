---
title: 230.二叉搜索树中第K小的元素（Kth Smallest Element in a BST）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [230\. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

Difficulty: **中等**


给定一个二叉搜索树，编写一个函数 `kthSmallest` 来查找其中第 **k **个最小的元素。

**说明：**
你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。

**示例 1:**

```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 1
```

**示例 2:**

```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 3
```

**进阶：**
如果二叉搜索树经常被修改（插入/删除操作）并且你需要频繁地查找第 k 小的值，你将如何优化 `kthSmallest` 函数？


#### Solution1 - 中序遍历

Language: **Java**

```java
​class Solution {
    public int kthSmallest(TreeNode root, int k) {
        List<Integer> list = new ArrayList<>();
        inorder(root,list);
        return list.get(k-1);
    }

    public void inorder(TreeNode node ,List list){
         if(node !=null){
             inorder(node.left,list);
             list.add(node.val);
             inorder(node.right,list);
         }


    }
}

```

```java
class Solution {
    int res, k;
    public int kthSmallest(TreeNode root, int k) {
        this.k = k;
        inorder(root, k);
        return res;
    }

    public void inorder(TreeNode root, int k){
            if (root == null || this.k < 1) {
                return;
            }
            inorder(root.left, k);
            if (this.k < 1) return;
            if (this.k-- == 1){
                res = root.val;
                return;
            }
            if (this.k < 1) return;
            inorder(root.right, k);
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)
[zhulg](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/solution/gen-ju-er-cha-shu-sou-suo-shu-te-zheng-zhong-xu-ji/)***
