---
title: 43. 字符串相乘（Multiply Strings）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个以字符串形式表示的非负整数 num1 和 num2，返回 num1 和 num2 的乘积，它们的乘积也表示为字符串形式。

示例 1:
```
输入: num1 = "2", num2 = "3"
输出: "6"
```
示例 2:
```
输入: num1 = "123", num2 = "456"
输出: "56088"
```
**说明：**
1. num1 和 num2 的长度小于110。
2. num1 和 num2 只包含数字 0-9。
3. num1 和 num2 均不以零开头，除非是数字 0 本身。
4. 不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。


# 题解

## 官方题解
暂无

## 其他题解
### 1.平行乘法
**思路：**
1. 从低到高位计算出每一行的乘积字符串。
2. 将计算出的每一行乘积字符串补上合适个数的 0 ，并保存起来。
3. 对所有的乘积字符串进行字符串加法运算。（融合操作类似于合并 k 个有序链表，可以自行优化）

也就是把两个横线中的字符串加上合适 0 后，合并起来。
![](https://i.loli.net/2019/09/15/dZeqDKmj5vITb13.png)


```
class Solution {
    public String multiply(String num1, String num2) {
        if(num1 == null || num1.length() == 0) return "0";
        if("0".equals(num1) || "0".equals(num2)) return "0";

        String[] results = new String[num1.length()];
        for(int i = num1.length() - 1; i >= 0; i --) {
            int n1Val = num1.charAt(i) - '0';
            int carry = 0;
            StringBuilder cur = new StringBuilder();
            for(int j = num2.length() - 1; j >= 0; j --) {
                int n2Val = num2.charAt(j) - '0';
                int sum = carry + n1Val * n2Val;
                carry = sum / 10;
                cur.append(sum % 10);
            }

            cur.append(carry != 0 ? carry : "");
            results[i] = cur.reverse().append(generateZero(num1.length() - i - 1)).toString();
        }

        // 这一部分融合操作可以优化成 分治 算法，效率更高。
        // 类似于合并 k 个有序链表。
        // 这里简单起见，我并没有优化，感兴趣的同学可以做一下优化。
        String res = results[0];
        for(int i = 1; i < results.length; i ++) {
            res = addStrings(res, results[i]);
        }

        return res;
    }

    private String generateZero(int n) {
        char[] zeros = new char[n];
        Arrays.fill(zeros, '0');
        return new String(zeros);
    }

    private String addStrings(String num1, String num2) {
        StringBuilder res = new StringBuilder();
        int carry = 0;
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        while(i >= 0 || j >= 0 || carry != 0) {
            int num1Val = i >= 0 ? num1.charAt(i) - '0' : 0;
            int num2Val = j >= 0 ? num2.charAt(j) - '0' : 0;
            int sum = carry + num1Val + num2Val;
            carry = sum / 10;

            res.append(sum % 10);

            if(i >= 0) i --;
            if(j >= 0) j --;
        }

        return res.reverse().toString();
    }
}
```
**复杂度分析**

### 2.竖式乘法
**思路：** 我们需要先知道：**两个数字相乘，最后的结果的长度必然小于两者的长度之和。**
这个和平行乘法一样，都是用了两数相乘的原理，只不过平行乘法是字符串单个乘出来后字符串才相加，竖式乘法是字符串单个乘出来储存在数组中，与下一个结果直接相加。简化了时间和空间复杂度。

> new String(ret, i, ret.length - i);
> 第三个参数是从 i 往后保留几个字符
```
class Solution {
    public String multiply(String num1, String num2) {

        char[] ret = new char[num1.length() + num2.length()];
        Arrays.fill(ret, '0');

        for(int i = num1.length() - 1; i >= 0; i --) {
            int num1Val = num1.charAt(i) - '0';
            for(int j = num2.length() - 1; j >= 0; j --) {
                int num2Val = num2.charAt(j) - '0';
                int sum = (ret[i + j + 1] - '0') + num1Val * num2Val;
                ret[i + j + 1] = (char)(sum % 10 + '0');
                ret[i + j] += sum / 10;
            }
        }

        for(int i = 0; i < ret.length; i ++) {
            if(ret[i] != '0' || i == ret.length - 1) {
                return new String(ret, i, ret.length - i);
            }
        }

        return "0";
    }
}
```
**复杂度分析**


---
***参考：
[simplehippo](https://leetcode-cn.com/problems/multiply-strings/solution/ping-xing-cheng-fa-yu-shu-shi-cheng-fa-by-simple-2/)***
