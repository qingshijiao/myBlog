---
title: 536. 从字符串生成二叉树

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目

![](https://img-blog.csdnimg.cn/20191111194158631.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0Z1ZGFucXFxcXE=,size_16,color_FFFFFF,t_70)


#### Solution

Language: **c++**
```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* str2tree(string s) {
        s+=')';
        int len=s.size();
        if(len==1){return 0;}
        int flag=1,temp=0;
        stack<TreeNode*> sta;
        TreeNode* root=new TreeNode(0);
        sta.push(root);
        TreeNode* cur=0,*par=0;
        for(int i=0;i<len;++i){
            if(s[i]=='('){
                ;
            }
            else if(s[i]==')'){
                cur=sta.top();
                sta.pop();
                par=sta.top();
                if(par->left){
                   par->right=cur;
                }
                else{
                    par->left=cur;
                }
            }
            else if(s[i]=='-'){
                flag=-1;
            }
            else{   //s[i]为数字
                temp=temp*10+(s[i]-'0');
                if(s[i+1]==')' or s[i+1]=='('){
                    cur=new TreeNode(temp*flag);
                    sta.push(cur);
                    flag=1,temp=0;
                }
            }
        }
        return root->left;
    }
};

```

---
***参考：
[Fudanqqqqq](https://blog.csdn.net/Fudanqqqqq/article/details/103016260)***
