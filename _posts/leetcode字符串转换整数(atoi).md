---
title: 8.字符串转换整数(atoi)（String to Integer (atoi))

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
请你来实现一个 *atoi* 函数，使其能将字符串转换成整数。

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

**说明：**

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−231,  231 − 1]。如果数值超过这个范围，qing返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

示例 1:
> 输入: "42"
> 输出: 42

示例 2:
> 输入: "   -42"
> 输出: -42
> 解释: 第一个非空白字符为 '-', 它是一个负号。
>      我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。

示例 3:
> 输入: "4193 with words"
> 输出: 4193
> 解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。

示例 4:
> 输入: "words and 987"
> 输出: 0
> 解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
>      因此无法执行有效的转换。

示例 5:
> 输入: "-91283472332"
> 输出: -2147483648
> 解释: 数字 "-91283472332" 超过 32 位有符号整数范围。
>      因此返回 INT_MIN (−231) 。




# 题解

## 官方题解
暂无

## 其他题解
### 1.非正则表达式
**思路：** 对字符串进行排查，先找到起始位置，依次输出，最后检查是否越界。
```
public int myAtoi(String str) {
  if (str == null) {
    return 0;
  }
  int len = str.length();
  boolean start = false;
  long res = 0;
  int flag = 1;
  for (int i = 0; i < len; i++) {
    char ch = str.charAt(i);
    if (start) {
      if (ch < '0' || ch > '9') {
        break;
      }
      res = res * 10 + (int) ch - 48;
      if (res * flag > Integer.MAX_VALUE) {
        return Integer.MAX_VALUE;
      }
      if (res * flag < Integer.MIN_VALUE) {
        return Integer.MIN_VALUE;
      }
    } else {
      if (ch == ' ') {
        continue;
      }
      if (ch == '-') {
        flag = -1;
      } else if (ch == '+') {
        flag = 1;
      } else if (ch < '0' || ch > '9') {
        return 0;
      } else {
        res = (int) ch - 48;
      }
      start = true;
    }

  }
  return (int) res * flag;
}
```

### 2.正则表达式
**思路：** 使用正则表达式快速识别字符串。
[java正则表达式](https://www.runoob.com/java/java-regular-expressions.html)
![](https://i.loli.net/2019/08/13/LsG4wJgdiXoKTtu.png)
解释一下正则表达式含义（为什么是双斜杠，这是java正则表达式需要有两个反斜杠才能被解析为其他语言中的转义作用。）
```
^[\\+\\-]?\\d+

^ 表示匹配字符串开头，我们匹配的就是 '+'  '-'  号

[] 表示匹配包含的任一字符，比如[0-9]就是匹配数字字符 0 - 9 中的一个

? 表示前面一个字符出现零次或者一次，这里用 ? 是因为 '+' 号可以省略

 \\d 表示一个数字 0 - 9 范围

+ 表示前面一个字符出现一次或者多次，\\d+ 合一起就能匹配一连串数字了
```
![](https://i.loli.net/2019/08/13/A291nGughytzUkC.png)
```
//需要导包
import java.util.regex.*;
public int myAtoi(String str) {
    //清空字符串开头和末尾空格（这是trim方法功能，事实上我们只需清空开头空格）
    str = str.trim();
    //java正则表达式
    Pattern p = Pattern.compile("^[\\+|\\-]?\\d+");
    Matcher m = p.matcher(str);
    int value = 0;
    //判断是否能匹配
    if (m.find()){
        //字符串转整数，溢出
        try {
            value = Integer.parseInt(str.substring(m.start(), m.end()));
        } catch (Exception e){
            //由于有的字符串"42"没有正号，所以我们判断'-'
            value = str.charAt(0) == '-' ? Integer.MIN_VALUE: Integer.MAX_VALUE;
        }
    }
    return value;
}
```

---
***参考：[领扣](https://leetcode-cn.com/problems/string-to-integer-atoi/solution/python-1xing-zheng-ze-biao-da-shi-by-knifezhu/)***
