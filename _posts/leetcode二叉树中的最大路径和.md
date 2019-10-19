---
title: 124.二叉树中的最大路径和（Binary Tree Maximum Path Sum）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个非空二叉树，返回其最大路径和。

本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。该路径至少包含一个节点，且不一定经过根节点。

示例 1:
```
输入: [1,2,3]

       1
      / \
     2   3

输出: 6
```
示例 2:
```
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

输出: 42
```

# 题解

## 官方题解
### 1.递归
**思路：**
![](https://pic.leetcode-cn.com/45568450c1b869362937807e70ebb3c287380e9eaf78ae3600040ad83cb7a267-124_gains.png)
![](https://pic.leetcode-cn.com/f5c2c1de7252473f7030373375edf4c8ca5e791f4b91fb8d314e39adb77b3bf9-124_max_path.png)

```
class Solution {
  int max_sum = Integer.MIN_VALUE;

  public int max_gain(TreeNode node) {
    if (node == null) return 0;

    // max sum on the left and right sub-trees of node
    int left_gain = Math.max(max_gain(node.left), 0);
    int right_gain = Math.max(max_gain(node.right), 0);

    // the price to start a new path where `node` is a highest node
    int price_newpath = node.val + left_gain + right_gain;

    // update max_sum if it's better to start a new path
    max_sum = Math.max(max_sum, price_newpath);

    // for recursion :
    // return the max gain if continue the same path
    return node.val + Math.max(left_gain, right_gain);
  }

  public int maxPathSum(TreeNode root) {
    max_gain(root);
    return max_sum;
  }
}
```
**复杂度分析：**
- 时间复杂度：O(N) 其中 N 是结点个数。我们对每个节点访问不超过 2 次。
- 空间复杂度：O(log(N))。我们需要一个大小与树的高度相等的栈开销，对于二叉树空间开销是O(log(N))。


## 其他题解
暂无

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/solution/er-cha-shu-de-zui-da-lu-jing-he-by-leetcode/)***
