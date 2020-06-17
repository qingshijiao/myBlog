---
title: 481. 神奇字符串 (Magical String)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [481\. 神奇字符串](https://leetcode-cn.com/problems/magical-string/)

Difficulty: **中等**


神奇的字符串 **S **只包含 '1' 和 '2'，并遵守以下规则：

字符串 **S** 是神奇的，因为串联字符 '1' 和 '2' 的连续出现次数会生成字符串 **S** 本身。

字符串 **S **的前几个元素如下：**S** = “1221121221221121122 ......”

如果我们将 **S** 中连续的 1 和 2 进行分组，它将变成：

1 22 11 2 1 22 1 22 11 2 11 22 ......

并且每个组中 '1' 或 '2' 的出现次数分别是：

1 2 2 1 1 2 1 2 2 1 2 2 ......

你可以看到上面的出现次数就是 **S** 本身。

给定一个整数 N 作为输入，返回神奇字符串 **S **中前 N 个数字中的 '1' 的数目。

**注意：**N 不会超过 100,000。

**示例：**

```
输入：6
输出：3
解释：神奇字符串 S 的前 6 个元素是 “12211”，它包含三个 1，因此返回 3。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int magicalString(int n) {
        if(n == 0) return 0;
        if(n <= 3) return 1;
        int[] res = new int[n];
        boolean flag = true;//此时为2
        res[0] = 1;
        res[1] = 2;
        res[2] = 2;
        int count = 1;
        int index = 3;
        int pos = 2;
        while (index < n){
            int m = res[pos];
            if(flag){
                for (int i = 0; i < m; i++) {
                    if(index < n){
                        res[index++] = 1;
                        count++ ;
                    }

                }
                flag = false;
            }else {
                for (int i = 0; i < m; i++) {
                    if(index < n){
                        res[index++] = 2;
                    }
                }
                flag = true;
            }
            pos ++ ;
        }
        return count;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/magical-string/)***
