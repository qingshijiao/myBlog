---
title: 297.二叉树的序列化与反序列化(Serialize and Deserialize Binary Tree)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [297\. 二叉树的序列化与反序列化](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)

Difficulty: **困难**


序列化是将一个数据结构或者对象转换为连续的比特位的操作，进而可以将转换后的数据存储在一个文件或者内存中，同时也可以通过网络传输到另一个计算机环境，采取相反方式重构得到原数据。

请设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

**示例: **

```
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

**提示: **这与 LeetCode 目前使用的方式一致，详情请参阅 。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

**说明: **不要使用类的成员 / 全局 / 静态变量来存储状态，你的序列化和反序列化算法应该是无状态的。


#### Solution

Language: **Java**

```java
​public class Codec {

    public String serialize(TreeNode root) {
        if (root == null) return null;
        StringBuilder sb = new StringBuilder();
        serializeByDLR(root, sb);
        return sb.toString();
    }

    void serializeByDLR(TreeNode root, StringBuilder sb) {
        if (root == null) {
            sb.append(',');
            return;
        }
        sb.append(root.val).append(',');
        serializeByDLR(root.left, sb);
        serializeByDLR(root.right, sb);
    }

    public TreeNode deserialize(String data) {
        if (data == null || data.length() == 0) return null;
        return deserializeByDLR(data, new int[1]);
    }

    TreeNode deserializeByDLR(String data, int[] i) {
        if (i[0] >= data.length()) return null;
        char ch = data.charAt(i[0]);
        if (ch == ',') {
            i[0]++;
            return null;
        }

        int val = 0;
        boolean negative = ch == '-';
        if (negative) i[0]++;
        while (i[0] < data.length() && (ch = data.charAt(i[0]++)) != ',') {
            val *= 10;
            val += Character.digit(ch, 10);
        }
        val = negative ? -val : val;

        TreeNode node = new TreeNode(val);
        node.left = deserializeByDLR(data, i);
        node.right = deserializeByDLR(data, i);
        return node;
    }
}
```

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    private TreeNode root;
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        this.root = root;
        return null;
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        return root;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/)***
