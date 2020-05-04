---
title: 396.旋转函数 (Rotate Function)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [396\. 旋转函数](https://leetcode-cn.com/problems/rotate-function/)

Difficulty: **中等**


给定一个长度为 _n_ 的整数数组 `A` 。

假设 `B<sub style="display: inline;">k</sub>` 是数组 `A` 顺时针旋转 _k_ 个位置后的数组，我们定义 `A` 的“旋转函数” `F` 为：

`F(k) = 0 * B<sub style="display: inline;">k</sub>[0] + 1 * B<sub style="display: inline;">k</sub>[1] + ... + (n-1) * B<sub style="display: inline;">k</sub>[n-1]`。

计算`F(0), F(1), ..., F(n-1)`中的最大值。

**注意:**
可以认为 _n_ 的值小于 10<sup>5</sup>。

**示例:**

```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

所以 F(0), F(1), F(2), F(3) 中的最大值是 F(3) = 26 。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int maxRotateFunction(int[] A) {
        int len = A.length;
        int sum = 0;
        int f0 = 0;
        for (int i = 0; i < len; i++) {
        sum += A[i];
        f0 += i * A[i];
        }

        if (len <= 1) {
        return f0;
        }

        int[] charg = new int[len - 1];
        for (int i = 0; i < len - 1; i++) {
        int temp = len * A[len - 1 - i] - sum;
        charg[i] = temp;
        }

        int maxValue = f0;
        int tempValue = f0;
        for (int i = 0; i < len - 1; i++) {
        tempValue = tempValue - charg[i];
        if (maxValue < tempValue) {
            maxValue = tempValue;
        }
        }

        return maxValue;
    }
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/rotate-function/submissions/)***
