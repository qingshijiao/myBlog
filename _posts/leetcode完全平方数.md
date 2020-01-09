---
title: 279.完全平方数（Perfect Squares）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [279\. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

Difficulty: **中等**


给定正整数 _n_，找到若干个完全平方数（比如 `1, 4, 9, 16, ...`）使得它们的和等于 _n_。你需要让组成和的完全平方数的个数最少。

**示例 1:**

```
输入: n = 12
输出: 3
解释: 12 = 4 + 4 + 4.
```

**示例 2:**

```
输入: n = 13
输出: 2
解释: 13 = 4 + 9.
```


#### Solution1 - 数学

Language: **Java**

```java
​class Solution {
 public int numSquares(int n) {
		while (n % 4 == 0)
			n /= 4;
		if (n % 8 == 7)
			return 4;
		for (int a = 0; a * a <= n; ++a) {
			int b = (int) Math.sqrt(n - a * a);
			if (a * a + b * b == n) {
				if (a == 0) {
					return 1;
				}
				return 2;
			}
		}
		return 3;
	}
}
```

```java
class Solution {
public int numSquares(int n) {
        if(n <= 0){return 0;}
        if(check1(n)){
            return 1;
        }else if(check2(n)){
            return 2;
        }else if(check3(n)){
            return 3;
        }else{
            return 4;
        }
    }
    public boolean check1(int n){
        int tem = (int)Math.sqrt(n);
        return tem*tem == n;
    }
    public boolean check2(int n){
        for(int i = 1 ; i * i < n ; i++){
            if(check1(n-i*i))
                return true;
        }
        return false;
    }
    public boolean check3(int n){
        for(int i = 1 ; i * i < n ; i++){
            if(check2(n-i*i)){
                return true;
            }
        }
        return false;
    }

}
```

#### Solution2 - 动态规划 / BFS
```java
class Solution {
    public int numSquares(int n) {
        // int[] dp = new int[n+1];
        // Arrays.fill(dp,n+2);
        // dp[0] = 0;
        // for(int i = 1;i <= n;i++)
        //     for(int j = 1;j * j <= i;j++){
        //         if(j * j <= i)
        //         dp[i] = Math.min(dp[i],dp[i - j * j] + 1);
        // }
        // return dp[n];
        //以上是动态规划解法

        boolean[] is = new boolean[n+1];
        Queue<Integer> queue = new LinkedList<Integer>();
        queue.offer(n);
        int step = 0;
        while(!queue.isEmpty()) {
            step++;
            int size = queue.size();
            for(int i = 0;i < size;i++) {
                int now = queue.poll();
                for(int j = 1;j * j <= now;j++) {
                    if(now - j * j == 0) return step;
                    if(is[now - j * j] == false) {
                        queue.offer(now - j * j);
                        is[now - j * j] = true;
                    }
                }
            }
        }
        return 0;
        // BFS 所有节点和其查为某数平方的为一条边，求N到0的最短距离
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/perfect-squares/)***
