---
title: 501. 二叉搜索树中的众数（Find Mode in Binary Search Tree）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [501\. 二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)

Difficulty: **简单**


给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

*   结点左子树中所含结点的值小于等于当前结点的值
*   结点右子树中所含结点的值大于等于当前结点的值
*   左子树和右子树都是二叉搜索树

例如：  
给定 BST `[1,null,2,2]`,

```
   1
    \
     2
    /
   2
```

`返回[2]`.

**提示**：如果众数超过1个，不需考虑输出顺序

**进阶：**你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）


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
    private int max = 0, c = 1;
    private TreeNode prev = null;
    private List<Integer> list = new LinkedList<>();
    public int[] findMode(TreeNode root) {
        findModes(root);
        int[] data = new int[list.size()];
        for(int i = 0; i<list.size();i++){
            data[i] = list.get(i);
        }
        return data;
    }

    public void findModes(TreeNode node) {
        if (node == null) {
            return;
        }
        findModes(node.left);
        if (prev != null){
            if(node.val == prev.val) {
                c += 1;
            }else{
                c = 1;
            }
        }
        if(c == max){
            list.add(node.val);
        }else if(c > max){
            list.clear();
            list.add(node.val);
            max = c;
        }
        prev = node;
        findModes(node.right);
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/submissions/)***
