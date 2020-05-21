---
title: 429. N叉树的层序遍历（N-ary Tree Level Order Traversal）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [429\. N叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

Difficulty: **中等**


给定一个 N 叉树，返回其节点值的_层序遍历_。 (即从左到右，逐层遍历)。

例如，给定一个 `3叉树` :

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/12/narytreeexample.png)

返回其层序遍历:

```
[
     [1],
     [3,2,4],
     [5,6]
]
```

**说明:**

1.  树的深度不会超过 `1000`。
2.  树的节点总数不会超过 `5000`。


#### Solution

Language: **Java**

```java
​/*
// Definition for a Node.
class Node {
    public int val;
    public List<Node> children;

    public Node() {}

    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, List<Node> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
    List<List<Integer>> output = new ArrayList<>();

    public void helper(Node root, int level){
        if(output.size() <= level) {
            output.add(new ArrayList<Integer>());
        }
        output.get(level).add(root.val);
        for(Node item : root.children){
            helper(item, level + 1);
        }

    }
    public List<List<Integer>> levelOrder(Node root) {
        if(root != null) helper(root, 0);
        return output;   
    }
}
```
---
***参考：
[LeetCode](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/submissions/)***
