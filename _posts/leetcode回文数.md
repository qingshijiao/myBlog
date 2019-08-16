---
title: 9. 回文数（Palindrome Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:
> 输入: 121
> 输出: true

示例 2:
> 输入: -121
> 输出: false
> 解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

示例 3:
> 输入: 10
> 输出: false
> 解释: 从右向左读, 为 01 。因此它不是一个回文数。

**进阶:**
你能不将整数转为字符串来解决这个问题吗？


# 题解

## 官方题解
### 1.将数字转换成字符串
**思路：** 将数字转换成字符串，然后判断字符串是否为回文。

```
///简单粗暴，看看就行
class Solution {
    public boolean isPalindrome(int x) {
        String reversedStr = (new StringBuilder(x + "")).reverse().toString();
        return (x + "").equals(reversedStr);
    }
}
```

### 2.将数字的首尾取出来比较
**思路：** 类似定义两个指针，都是一个取首，一个取尾。
```
class Solution {
    public boolean isPalindrome(int x) {
        //边界判断
        if (x < 0) return false;
        //div保证了，当为个位数时保留数字
        int div = 1;
        //查看数字的位数
        while (x / div >= 10) div *= 10;
        while (x > 0) {
            int left = x / div;
            int right = x % 10;
            if (left != right) return false;
            //比较完把首尾两个数字去掉
            x = (x % div) / 10;
            div /= 100;
        }
        return true;
    }
}
```

### 3.只反转后半部分数字
**思路：** 由回文性质数字成中心对称，如果我们全部将其反转有可能溢出，所以我们只反转后一半，将其和前一半比较。
```
class Solution {
    public boolean isPalindrome(int x) {
        //因为0不可能作数字首部
        if (x < 0 || (x % 10 == 0 && x != 0)) return false;
        int revertedNumber = 0;
        //偶长度两者相等，奇长度反转数比原数大
        while (x > revertedNumber) {
            revertedNumber = revertedNumber * 10 + x % 10;
            x /= 10;
        }
        return x == revertedNumber || x == revertedNumber / 10;
    }
}
```

## 其他题解
暂无

---
***参考：
[领扣](https://leetcode-cn.com/problems/string-to-integer-atoi/solution/python-1xing-zheng-ze-biao-da-shi-by-knifezhu/)
[程序员小吴](https://leetcode-cn.com/problems/palindrome-number/solution/dong-hua-hui-wen-shu-de-san-chong-jie-fa-fa-jie-ch/)***
