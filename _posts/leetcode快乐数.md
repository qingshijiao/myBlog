---
title: 202.快乐数（Happy Number）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [201\. 数字范围按位与](https://leetcode-cn.com/problems/happy-number/)

Difficulty: **简单**


编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

**示例:**

```
输入: 19
输出: true
解释:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```


#### Solution1 - 双指针

Language: **Java**

```java
​class Solution {
    public int bitSquareSum(int n) {
        int sum = 0;
        while(n > 0)
        {
            int bit = n % 10;
            sum += bit * bit;
            n = n / 10;
        }
        return sum;
    }

    public boolean isHappy(int n) {
        int slow = n, fast = n;
        do{
            slow = bitSquareSum(slow);
            fast = bitSquareSum(fast);
            fast = bitSquareSum(fast);
        }while(slow != fast);

        return slow == 1;
    }
}
```

#### Solution2 - 判断运算次数

Language: **Java**

```java
​class Solution {
    public boolean isHappy(int n) {
          int res=0;
        int count=0;
        while(res!=1){
            res=0;//res 需要在每次循环置0

            while(n!=0){//每次循环判断数字是否为0
                res+=Math.pow((n%10),2);    //每位平方
                n=n/10;//取结果
            }
            n=res;  //更新原来的数字
            count++;
            if(count>10){
                return false;
            }
        }
        return true;
    }
}
```

#### Solution3 - 尾递归
- 不是快乐数的数称为不快乐数(unhappy number)，所有不快乐数的数位平方和计算，最后都会进入 4 → 16 → 37 → 58 → 89 → 145 → 42 → 20 → 4 的循环中
- 已知规律： [1 ~ 4] 中只有 1 是快乐数，[5 ~ ∞] 的数字要么回归到 1 要么回归到 4 或 3
- 因此仅需在 n > 4 时调用递归

Language: **Python**

```python
class Solution:
    def isHappy(self, n: int) -> bool:
        return self.isHappy(sum(int(i) ** 2 for i in str(n))) if n > 4 else n == 1

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/happy-number/)
[金字塔下的小蜗牛](https://leetcode-cn.com/problems/happy-number/solution/shi-yong-kuai-man-zhi-zhen-si-xiang-zhao-chu-xun-h/)***
