---
title: 366.寻找二叉树的叶子节点 (Find Leaves of Binary Tree)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
## 题目描述:##
给你一棵完全二叉树，请按以下要求的顺序收集它的全部节点：

依次从左到右，每次收集并删除所有的叶子节点
重复如上过程直到整棵树为空
示例:
```
输入: [1,2,3,4,5]
      1
     / \
    2   3
   / \
  4   5
输出: [[4,5,3],[2],[1]]
解释:

删除叶子节点 [4,5,3] ，得到如下树结构：
1 / 2
现在删去叶子节点 [2] ，得到如下树结构：
1
现在删去叶子节点 [1] ，得到空树：
[]

```
#### Solution

Language: **Java**

```java
​class Solution {
  public List<List<Integer>> findLeaves(TreeNode root) {
    List<List<Integer>> result = new ArrayList<List<Integer>>();
    helper(result, root);
    return result;
  }

  // traverse the tree bottom-up recursively
  private int helper(List<List<Integer>> list, TreeNode root){
    if(root==null)
        return -1;

    int left = helper(list, root.left);
    int right = helper(list, root.right);
    int curr = Math.max(left, right)+1;

    // the first time this code is reached is when curr==0,
    //since the tree is bottom-up processed.
    if(list.size()<=curr){
        list.add(new ArrayList<Integer>());
    }

    list.get(curr).add(root.val);

    return curr;
  }
}
```
---
***参考:
[lightwindy](https://www.cnblogs.com/lightwindy/p/9583763.html)***
