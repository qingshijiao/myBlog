---
title: 449. 序列化和反序列化二叉搜索树 (Serialize and Deserialize BST)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [449\. 序列化和反序列化二叉搜索树](https://leetcode-cn.com/problems/serialize-and-deserialize-bst/)

Difficulty: **中等**


序列化是将数据结构或对象转换为一系列位的过程，以便它可以存储在文件或内存缓冲区中，或通过网络连接链路传输，以便稍后在同一个或另一个计算机环境中重建。

设计一个算法来序列化和反序列化**二叉搜索树**。 对序列化/反序列化算法的工作方式没有限制。 您只需确保二叉搜索树可以序列化为字符串，并且可以将该字符串反序列化为最初的二叉搜索树。

**编码的字符串应尽可能紧凑。**

**注意**：不要使用类成员/全局/静态变量来存储状态。 你的序列化和反序列化算法应该是无状态的。


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
public class Codec {
 public int i = 0;

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        doSerialize(root, sb);
        return sb.toString();
    }

    public void doSerialize(TreeNode root, StringBuilder sb) {
        if (root == null) {
            return;
        }
        sb.append((char) root.val);
        doSerialize(root.left, sb);
        doSerialize(root.right, sb);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        char[] arr = data.toCharArray();
        return doDescrialize(arr, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }

    private TreeNode doDescrialize(char[] arr, int minValue, int maxValue) {
        if (i >= arr.length || (char) arr[i] > maxValue) {
            return null;
        }
        TreeNode root = new TreeNode((char) arr[i++]);
        root.left = doDescrialize(arr, minValue, root.val);
        root.right = doDescrialize(arr, root.val, maxValue);
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/serialize-and-deserialize-bst/)***
