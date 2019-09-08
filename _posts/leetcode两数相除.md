---
title: 29. 两数相除（Divide Two Integers）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定两个整数，被除数 dividend 和除数 divisor。将两数相除，要求不使用乘法、除法和 mod 运算符。

返回被除数 dividend 除以除数 divisor 得到的商。

示例 1:
> 输入: dividend = 10, divisor = 3
> 输出: 3

示例 2:
> 输入: dividend = 7, divisor = -3
> 输出: -2

**说明:**
- 被除数和除数均为 32 位有符号整数。
- 除数不为 0。
- 假设我们的环境只能存储 32 位有符号整数，其数值范围是 [−231,  231 − 1]。本题中，如果除法结果溢出，则返回 231 − 1。




# 题解

## 官方题解
暂无

## 其他题解
### 1.除数倍增
**思路：** 逐个字符判断，全部符合退出，不符合则字符前端向后移动一个单位。
> 63 = 32 + 16 + 8 + 4 + 2 + 1
> 我们都从除数 1 倍的 divisor 开始递增，知道 64 倍（假设）超出限制，
> tmpd += tmpd 实际就是扩大了两倍，也可以用位运算左移，tmpd = tmpd << 1
```
class Solution {
    public int divide(int dividend, int divisor) {
        if (dividend == Integer.MIN_VALUE && divisor == -1) return Integer.MAX_VALUE;

        int flag = 1; // 1 表示正数，-1表示负数；
        if (dividend > 0) {
            dividend = -dividend;
        } else {
            flag = -flag;
        }
        if (divisor > 0) {
            divisor = -divisor;
        } else {
            flag = -flag;
        }

        int s = 0, tmpd, k;
        while (dividend <= divisor) {
            tmpd = divisor;
            k = 1;
            while (dividend <= tmpd + tmpd && tmpd + tmpd < 0) {
                tmpd += tmpd;
                k += k;
            }
            s = s + k;
            dividend -= tmpd;
        }
        return flag > 0 ? s : -s;
    }
}
```

### 2.竖式除法
**思路：** 根据除法原理，将十进制除法竖式转换为二进制除法竖式。
> Math.abs(-2147483648)输出为-2147483648
[知乎](https://www.zhihu.com/question/51632291)
```
class Solution {
    public int divide(int dividend, int divisor) {
        if (divisor == 1){
            return dividend;
        }
        if (dividend == Integer.MIN_VALUE && divisor == -1){
            return Integer.MAX_VALUE;
        }
        boolean flag = (dividend > 0)  ^  (divisor > 0);
        long m = Math.abs((long)dividend);
        long n = Math.abs((long)divisor);
        int ans = 0;

        for (int i = 31; i >= 0; i--){
            if ((m >> i) >= n){
                ans += 1 << i;
                System.out.print(ans + " ");
                m -= n << i;
            }
        }
        return flag? -ans: ans;
    }
}
```

---
***参考：
[ysy4869](https://leetcode-cn.com/problems/divide-two-integers/solution/xiao-xue-sheng-du-hui-de-lie-shu-shi-suan-chu-fa-b/)
[heator](https://leetcode-cn.com/problems/divide-two-integers/solution/javachu-shu-bei-zeng-die-dai-xun-huan-bu-shi-yong-/)***
