---
title: 374.猜数字大小 (Guess Number Higher or Lower)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [374\. 猜数字大小](https://leetcode-cn.com/problems/guess-number-higher-or-lower/)

Difficulty: **简单**


我们正在玩一个猜数字游戏。 游戏规则如下：
我从 **1** 到 _**n**_ 选择一个数字。 你需要猜我选择了哪个数字。
每次你猜错了，我会告诉你这个数字是大了还是小了。
你调用一个预先定义好的接口 `guess(int num)`，它会返回 3 个可能的结果（`-1`，`1` 或 `0`）：

```
-1 : 我的数字比较小
 1 : 我的数字比较大
 0 : 恭喜！你猜对了！
```

**示例 :**

```
输入: n = 10, pick = 6
输出: 6
```


#### Solution

Language: **Java**

```java
​/**
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is lower than the guess number
 *			      1 if num is higher than the guess number
 *               otherwise return 0
 * int guess(int num);
 */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int left = 1;
        int right = n;
        while(left < right){
            int mid = left + (right -left) / 2;
            int result = guess(mid);
            if(result == -1) {
                right = mid;
            }
            else if(result == 1) {
                left = mid + 1;
            }
            else {
                return mid;
            }
        }
        return left;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/guess-number-higher-or-lower/submissions/)***
