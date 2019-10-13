---
title: 108.将有序数组转换为二叉搜索树（Convert Sorted Array to Binary Search Tree）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
将一个按照升序排列的有序数组，转换为一棵高度平衡二叉搜索树。

本题中，一个高度平衡二叉树是指一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。

示例:

给定有序数组: [-10,-3,0,5,9],

一个可能的答案是：[0,-3,9,-10,null,5]，它可以表示下面这个高度平衡二叉搜索树：
```
      0
     / \
   -3   9
   /   /
 -10  5
```



# 题解

## 官方题解
暂无


## 其他题解
### 1.递归
**思路：**


```
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
    public TreeNode sortedArrayToBST(int[] nums) {
        return sortedArrayToBST(nums, 0, nums.length);
    }

    private TreeNode sortedArrayToBST(int[] nums, int start, int end) {
        if (start == end) {
            return null;
        }
        int mid = (start + end) >>> 1;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = sortedArrayToBST(nums, start, mid);
        root.right = sortedArrayToBST(nums, mid + 1, end);

        return root;
    }
}
```

### 2.栈 DFS
**思路：**
[java移位运算符](https://zhuanlan.zhihu.com/p/30108890)
**正数的原码反码补码均相同**
假如符号位为 0，下一位是 1，溢出时 0 会被丢弃，>> 补位为 1，>>> 补位位 0，还是正数。
```
其实问题的关键就是这里了>>> ，我们知道还有一种右移是>>。区别在于>>为有符号右移，右移以后最高位保持原来的最高位。而>>>这个右移的话最高位补 0。

所以这里其实利用到了整数的补码形式，最高位其实是符号位，所以当 start + end溢出的时候，其实本质上只是符号位收到了进位，而>>>这个右移可以带着符号位右移，所以之前的信息没有丢掉。

```
```
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
    class MyTreeNode {
        TreeNode root;
        int start;
        int end;

        MyTreeNode(TreeNode r, int s, int e) {
            this.root = r;
            this.start = s;
            this.end = e;
        }
    }
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums.length == 0) {
            return null;
        }
        Stack<MyTreeNode> rootStack = new Stack<>();
        int start = 0;
        int end = nums.length;
        int mid = (start + end) >>> 1;
        TreeNode root = new TreeNode(nums[mid]);
        TreeNode curRoot = root;
        rootStack.push(new MyTreeNode(root, start, end));
        while (end - start > 1 || !rootStack.isEmpty()) {
            //考虑左子树
            while (end - start > 1) {
                mid = (start + end) >>> 1; //当前根节点
                end = mid;//左子树的结尾
                mid = (start + end) >>> 1;//左子树的中点
                curRoot.left = new TreeNode(nums[mid]);
                curRoot = curRoot.left;
                rootStack.push(new MyTreeNode(curRoot, start, end));
            }
            //出栈考虑右子树
            MyTreeNode myNode = rootStack.pop();
            //当前作为根节点的 start end 以及 mid
            start = myNode.start;
            end = myNode.end;
            mid = (start + end) >>> 1;
            start = mid + 1; //右子树的 start
            curRoot = myNode.root; //当前根节点
            if (start < end) { //判断当前范围内是否有数
                mid = (start + end) >>> 1; //右子树的 mid
                curRoot.right = new TreeNode(nums[mid]);
                curRoot = curRoot.right;
                rootStack.push(new MyTreeNode(curRoot, start, end));
            }

        }

        return root;
    }
}
```

### 3.队列 BFS
**思路：**

```
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
    class MyTreeNode {
        TreeNode root;
        int start;
        int end;

        MyTreeNode(TreeNode r, int s, int e) {
            this.root = r;
            this.start = s;
            this.end = e;
        }
    }


    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums.length == 0) {
            return null;
        }
        Queue<MyTreeNode> rootQueue = new LinkedList<>();
        TreeNode root = new TreeNode(0);
        rootQueue.offer(new MyTreeNode(root, 0, nums.length));
        while (!rootQueue.isEmpty()) {
            MyTreeNode myRoot = rootQueue.poll();
            int start = myRoot.start;
            int end = myRoot.end;
            int mid = (start + end) >>> 1;
            TreeNode curRoot = myRoot.root;
            curRoot.val = nums[mid];
            if (start < mid) {
                curRoot.left = new TreeNode(0);
                rootQueue.offer(new MyTreeNode(curRoot.left, start, mid));
            }
            if (mid + 1 < end) {
                curRoot.right = new TreeNode(0);
                rootQueue.offer(new MyTreeNode(curRoot.right, mid + 1, end));
            }
        }

        return root;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/submissions/)
[windliang](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-24/)***
