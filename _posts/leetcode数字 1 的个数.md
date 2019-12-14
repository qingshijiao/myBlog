---
title: 233.数字 1 的个数（Number of Digit One）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [233\. 数字 1 的个数](https://leetcode-cn.com/problems/number-of-digit-one/)

Difficulty: **困难**


给定一个整数 n，计算所有小于等于 n 的非负整数中数字 1 出现的个数。

**示例:**

```
输入: 13
输出: 6
解释: 数字 1 出现在以下数字中: 1, 10, 11, 12, 13 。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public int countDigitOne(int n) {
        int cnt = 0;
	    int mul =1;
	    int left =n;
	    int right =0;
	    if(n==0) {
	    	return 0;
	    }
	    while(left>0) {
	    	int digit = left%10;
	    	left/=10;
	    	if(digit == 1) {
	    		cnt+=left*mul;
	    		cnt+=right+1;
	    	}
	    	else if(digit<1) {
	    		cnt+=left*mul;
	    	}
	    	else {
	    		cnt+=(left+1)*mul;
	    	}
	    	right+=digit*mul;
	    	mul*=10;
	    }
		return cnt;
    }
}
```

通用版
```java
private static int count(int n, int x) {
		int cnt = 0;
	    int mul =1;
	    int left =n;
	    int right =0;
	    if(n==0) {
	    	return x<1?n:0;
	    }
	    while(left>0) {
	    	int digit = left%10;
	    	left/=10;
	    	if(digit == x) {
	    		cnt+=left*mul;
	    		cnt+=right+1;
	    	}
	    	else if(digit<x) {
	    		cnt+=left*mul;
	    	}
	    	else {
	    		cnt+=(left+1)*mul;
	    	}
	    	if(x == 0&&mul>1) {
	    		cnt-=mul;
	    	}
	    	right+=digit*mul;
	    	mul*=10;
	    }
		return cnt;
		}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/number-of-digit-one/solution/shu-zi-1-de-ge-shu-by-leetcode/)
[wzq_love_zxj](https://leetcode-cn.com/problems/number-of-digit-one/solution/javaban-shu-zi-1de-ge-shu-tong-yong-ban-by-wzq_lov/)***
