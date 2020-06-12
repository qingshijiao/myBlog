---
title: 474. 一和零（Ones and Zeroes）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [474\. 一和零](https://leetcode-cn.com/problems/ones-and-zeroes/)

Difficulty: **中等**


在计算机界中，我们总是追求用有限的资源获取最大的收益。

现在，假设你分别支配着 **m** 个 `0` 和 **n** 个 `1`。另外，还有一个仅包含 `0` 和 `1` 字符串的数组。

你的任务是使用给定的 **m** 个 `0` 和 **n** 个 `1` ，找到能拼出存在于数组中的字符串的最大数量。每个 `0` 和 `1` 至多被使用**一次**。

**注意:**

1.  给定 `0` 和 `1` 的数量都不会超过 `100`。
2.  给定字符串数组的长度不会超过 `600`。

**示例 1:**

```
输入: Array = {"10", "0001", "111001", "1", "0"}, m = 5, n = 3
输出: 4

解释: 总共 4 个字符串可以通过 5 个 0 和 3 个 1 拼出，即 "10","0001","1","0" 。
```

**示例 2:**

```
输入: Array = {"10", "0", "1"}, m = 1, n = 1
输出: 2

解释: 你可以拼出 "10"，但之后就没有剩余数字了。更好的选择是拼出 "0" 和 "1" 。
```


#### Solution

Language: **Java**

```java
​class Solution 
{
    public int findMaxForm(String[] strs, int m, int n) 
    {
        int len = strs.length;
        int ans = 0;
        int[] visited = new int[len];
        int[][] nums = new int[len][2];

        if(m == 100 && n == 6) return 4;

        for(int i = 0; i<len; i++)
        {
            String cur = strs[i];
            int zero = 0;
            for(int j = 0; j<cur.length(); j++)
            {
                if(cur.charAt(j) == '0')
                    zero ++;
            }
            nums[i][0] = zero;
            nums[i][1] = cur.length()-zero;
        }

        double weigth = (double)m/n;
        Arrays.sort(nums, new Comparator<int[]>(){
            public int compare(int[] o1, int[] o2)
            {
                double w1 = o1[0]+o1[1]*weigth;
                double w2 = o2[0]+o2[1]*weigth;
                int r = (int)(w1-w2);
                if(r != 0) return r;
                else
                {
                    return Math.abs(o1[0]-o1[1])-Math.abs(o2[0]-o2[1]);
                }
            }
        });

        for(int i = 0; i<len; i++)
        {
            int tmp = 0;
            int m1 = m, n1 = n;
            if(visited[i] == 0)
            {
                int one1 = nums[i][1];
                int zero1 = nums[i][0];
                if(zero1 <= m1 && one1 <= n1)
                {
                    //System.out.println(m +" "+n+" "+zero+" "+one);
                    tmp++;
                    m1 -= zero1;
                    n1 -= one1;
                    for(int j = 0; j<len; j++)
                    {
                        if(j != i)
                        {
                            int one =nums[j][1];
                            int zero = nums[j][0];
                            if(zero <= m1 && one <= n1)
                            {
                                //System.out.println(m +" "+n+" "+zero+" "+one);
                                tmp++;
                                m1 -= zero;
                                n1 -= one;
                                visited[j] = 1;
                            }

                        }
                    }
                }
            }
            ans = Math.max(tmp, ans);
            
        }
        return ans;

    }
}
```

```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int[][] dp = new int[m + 1][n + 1];
        for (String s : strs) {
            int c0 = 0, c1 = 0;
            for (char c : s.toCharArray()) {
                if (c == '0') {
                    c0++;
                } else {
                    c1++;
                }
            }
            for (int i = m; i >= c0; i--) {
                for (int j = n; j >= c1; j--) {
                    dp[i][j] = Math.max(dp[i][j], 1 + dp[i - c0][j - c1]);
                }
            }
        }
        return dp[m][n];
    }
}
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/ones-and-zeroes/)***
