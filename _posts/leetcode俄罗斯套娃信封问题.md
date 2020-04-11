---
title: 354.俄罗斯套娃信封问题 (Russian Doll Envelopes)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [354\. 俄罗斯套娃信封问题](https://leetcode-cn.com/problems/russian-doll-envelopes/)

Difficulty: **困难**


给定一些标记了宽度和高度的信封，宽度和高度以整数对形式 `(w, h)` 出现。当另一个信封的宽度和高度都比这个信封大的时候，这个信封就可以放进另一个信封里，如同俄罗斯套娃一样。

请计算最多能有多少个信封能组成一组“俄罗斯套娃”信封（即可以把一个信封放到另一个信封里面）。

**说明:**
不允许旋转信封。

**示例:**

```
输入: envelopes = [[5,4],[6,4],[6,7],[2,3]]
输出: 3
解释: 最多信封的个数为 3, 组合为: [2,3] => [5,4] => [6,7]。
```


#### Solution - 排序 + 最长递增子序列

Language: **Java**

```java
​class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        if (envelopes.length <= 0) return 0;
        Arrays.sort(envelopes, new Comparator<int[]>() {
            @Override
            public int compare(int[] a, int[] b) {
                if (a[0] == b[0]) return b[1] - a[1];
                return a[0] - b[0];
            }
        });
        int[] dp = new int[envelopes.length];
        int len = 0;
        for (int i = 0; i < envelopes.length; i++) {
            if (len == 0) {
                dp[len] = envelopes[i][1];
                len++;
                continue;
            }
            int start = 0;
            int end = len - 1;
            while (start <= end) {
                int mid = start + (end - start) / 2;
                if (dp[mid] == envelopes[i][1]) {
                    start = mid;
                    break;
                } else if (dp[mid] > envelopes[i][1]) {
                    end = mid - 1;
                } else {
                    start = mid + 1;
                }
            }
            if (start == len) {
                len++;
            }
            dp[start] = envelopes[i][1];
        }
        return len;
    }
}
```


---
***参考:
[leetcode](https://leetcode-cn.com/problems/russian-doll-envelopes/solution/e-luo-si-tao-wa-xin-feng-wen-ti-by-leetcode/)***
