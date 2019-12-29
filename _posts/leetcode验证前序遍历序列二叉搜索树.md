---
title: 255.验证前序遍历序列二叉搜索树（Verify Preorder Sequence in Binary Search Tree）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Given an array of numbers, verify whether it is the correct preorder traversal sequence of a binary search tree.

You may assume each number in the sequence is unique.

Consider the following binary search tree:
```
     5
    / \
   2   6
  / \
 1   3
```
Example 1:
```
Input: [5,2,6,1,3]
Output: false
```
Example 2:
```
Input: [5,2,1,3,6]
Output: true
```
**Follow up:**
Could you do it using only constant space complexity?

#### Solution - 数组实现栈

Language: **Java**

```java
public class Solution {
    public boolean verifyPreorder(int[] preorder) {
        /*
        //Method 1
        int low = Integer.MIN_VALUE;
        Stack<Integer> stk = new Stack<Integer>();
        for(int num : preorder){
            if(num < low){
                return false;
            }
            while(!stk.isEmpty() && stk.peek() < num){
               low = stk.pop();
            }
            stk.push(num);
        }
        return true;
        */
        int index = -1;
        int low = Integer.MIN_VALUE;
        for(int num : preorder){
            if(num < low){
                return false;
            }
            while(index >= 0 && preorder[index] < num){
                low = preorder[index--];
            }
            preorder[++index] = num;
        }
        return true;
    }
}
```


---
***参考：
[Dylan_Java_NYC](https://www.cnblogs.com/Dylan-Java-NYC/p/5327638.html)***
