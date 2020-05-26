---
title: 437. 路径总和 III（Path Sum III）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [437\. 路径总和 III](https://leetcode-cn.com/problems/path-sum-iii/)

Difficulty: **简单**


给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。

**示例：**

```
root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

返回 3。和等于 8 的路径有:

1\.  5 -> 3
2\.  5 -> 2 -> 1
3\.  -3 -> 11
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
    public int pathSum(TreeNode root, int sum) {
        Map<Integer, Integer> prefixSum = new HashMap<>();
        prefixSum.put(0, 1);
        return pathSum(root, sum, prefixSum, 0);
    }
    private int pathSum(TreeNode node, int sum, Map<Integer, Integer> prefixSum, int currSum) {
        if (node == null) {
            return 0;
        }
        int res = 0;
        currSum += node.val;
        res += prefixSum.getOrDefault(currSum - sum, 0);
        prefixSum.put(currSum, prefixSum.getOrDefault(currSum, 0) + 1);
        
        res += pathSum(node.left, sum, prefixSum, currSum);
        res += pathSum(node.right, sum, prefixSum, currSum);
        
        prefixSum.put(currSum, prefixSum.get(currSum) - 1);
        return res;
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/path-sum-iii/)***
