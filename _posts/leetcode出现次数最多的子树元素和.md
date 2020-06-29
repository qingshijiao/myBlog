---
title: 508. 出现次数最多的子树元素和 (Most Frequent Subtree Sum)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [508\. 出现次数最多的子树元素和](https://leetcode-cn.com/problems/most-frequent-subtree-sum/)

Difficulty: **中等**


给你一个二叉树的根结点，请你找出出现次数最多的子树元素和。一个结点的「子树元素和」定义为以该结点为根的二叉树上所有结点的元素之和（包括结点本身）。

你需要返回出现次数最多的子树元素和。如果有多个元素出现的次数相同，返回所有出现次数最多的子树元素和（不限顺序）。

**示例 1：**  
输入:

```
  5
 /  \
2   -3
```

返回 [2, -3, 4]，所有的值均只出现一次，以任意顺序返回所有值。

**示例 2：**  
输入：

```
  5
 /  \
2   -5
```

返回 [2]，只有 2 出现两次，-5 只出现 1 次。

**提示：** 假设任意子树元素和均可以用 32 位有符号整数表示。


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
    int maxTime = 0;
    List<Integer> res;
    Map<Integer, Integer> map;
    public int[] findFrequentTreeSum(TreeNode root) {
        res = new ArrayList<>();
        map = new HashMap<>();
        dfs(root);
        int[] arr = new int[res.size()];
        for(int i = 0; i < arr.length; i++){
            arr[i] = res.get(i);
        }
        return arr;
    }
    private int dfs(TreeNode root){
        if(root == null){
            return 0;
        }
        int sum = root.val + dfs(root.left) + dfs(root.right);
        int time = map.getOrDefault(sum, 0) + 1;
        if(time >= maxTime){
            if(time > maxTime){
                maxTime = time;
                res.clear();
            }
            res.add(sum);
        }
        map.put(sum, time);
        return sum;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/most-frequent-subtree-sum/)***
