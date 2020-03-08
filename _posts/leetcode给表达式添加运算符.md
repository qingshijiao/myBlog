---
title: 282.给表达式添加运算符 (Expression Add Operators)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [282\. 给表达式添加运算符](https://leetcode-cn.com/problems/expression-add-operators/)

Difficulty: **困难**


给定一个仅包含数字 `0-9` 的字符串和一个目标值，在数字之间添加**二元**运算符（不是一元）`+`、`-` 或 `*` ，返回所有能够得到目标值的表达式。

**示例 1:**

```
输入: num = "123", target = 6
输出: ["1+2+3", "1*2*3"]
```

**示例 2:**

```
输入: num = "232", target = 8
输出: ["2*3+2", "2+3*2"]
```

**示例 3:**

```
输入: num = "105", target = 5
输出: ["1*0+5","10-5"]
```

**示例 4:**

```
输入: num = "00", target = 0
输出: ["0+0", "0-0", "0*0"]
```

**示例 5:**

```
输入: num = "3456237490", target = 9191
输出: []
```


#### Solution - 回溯

Language: **Java**

```java
class Solution {
   char[] num;
    char[] exp;
    int target;
    List<String> res;
    public List<String> addOperators(String num, int target) {
        this.res = new ArrayList<>();
        this.num = num.toCharArray();
        this.target = target;
        this.exp = new char[num.length()*2];
        dfs(0,0,0,0);
        return res;
    }

    private void dfs(int pos,int len,long prev,long curr) {
        if(pos == num.length) {
            if(curr==target) {
                res.add(new String(exp,0,len));
            }
            return;
        }
        /**
         * s 记录该次 dfs的起始位置
         * pos是num的位置
         */
        int s = pos;
        /**
         * len是 放数字 的位置
         * l是 放运算符 的位置
         */
        int l = len;
        if(s!=0) {
            len++;
        }
        long n = 0;
        while (pos < num.length){
            if(num[s] =='0' && pos-s>0) {
                break;
            }
            n = n*10+(int)(num[pos] -'0');
            if(n > Integer.MAX_VALUE){
                break;
            }
            exp[len++] = num[pos++];
            if(s==0) {
                dfs(pos,len,n,n);
                continue;
            }
            exp[l] = '+';
            dfs(pos,len,n,curr+n);
            exp[l] = '-';
            dfs(pos,len,-n,curr-n);
            exp[l] = '*';
            dfs(pos,len,prev*n,curr-prev+prev*n);
        }
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/expression-add-operators/solution/gei-biao-da-shi-tian-jia-yun-suan-fu-by-leetcode/)***
