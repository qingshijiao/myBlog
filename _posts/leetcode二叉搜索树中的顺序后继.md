---
title: 285.二叉搜索树中的顺序后继

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目描述
给你一个二叉搜索树和其中的某一个结点，请你找出该结点在树中顺序后继的节点。

结点 p 的后继是值比 p.val 大的结点中键值最小的结点。

示例 1:
![](https://img-blog.csdnimg.cn/2019072520034595.png)
```
输入: root = [2,1,3], p = 1
输出: 2
解析: 这里 1 的顺序后继是 2。请注意 p 和返回值都应是 TreeNode 类型。
```

示例 1:
![](https://img-blog.csdnimg.cn/20190725200353701.png)
```
输入: root = [5,3,6,2,4,null,null,1], p = 6
输出: null
解析: 因为给出的结点没有顺序后继，所以答案就返回 null 了。
```

*注意:*

- 假如给出的结点在该树中没有顺序后继的话，请返回 null
- 我们保证树中每个结点的值是唯一的


#### Solution - 中序遍历找到下一个节点pNext

Language: **Java**

```java
class Solution {
    TreeNode *pPrev = nullptr;
    TreeNode *pNext = nullptr;
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        if(!root || !p) return nullptr;
        inorder(root,p);
        return pNext;
    }

    void inorder(TreeNode* root, TreeNode *p){
        if(!root) return;
        inorder(root->left,p);
        if(pPrev && pPrev == p)
            pNext = root;
        pPrev = root;
        inorder(root->right, p);
    }
};

```


---
***参考：
[zjwreal](https://blog.csdn.net/zjwreal/article/details/97293780)***
