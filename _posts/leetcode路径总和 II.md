---
title: 113.路径总和 II（Path Sum II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

说明: 叶子节点是指没有子节点的节点。

示例:
给定如下二叉树，以及目标和 sum = 22，
```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
返回:
```
[
   [5,4,11,2],
   [5,8,4,5]
]
```


# 题解

## 官方题解
暂无

## 其他题解

### 1.DFS 递归
**思路：**
```
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        List<List<Integer>> res = new ArrayList<>();
        helper(root, sum, res, new ArrayList<Integer>());
        return res;
    }

    private void helper(TreeNode root, int sum, List<List<Integer>> res, ArrayList<Integer> tmp) {
        if (root == null) return;
        tmp.add(root.val);
        if (root.left == null && root.right == null && sum - root.val == 0) res.add(new ArrayList<>(tmp));
        helper(root.left, sum - root.val, res, tmp);
        helper(root.right, sum - root.val, res, tmp);
        tmp.remove(tmp.size() - 1);
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/path-sum-ii/submissions/)
[powcai](https://leetcode-cn.com/problems/path-sum-ii/solution/dfs-by-powcai-2/)***
