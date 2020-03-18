---
title: 303.区域和检索 - 数组不可变(Range Sum Query - Immutable)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [303\. 区域和检索 - 数组不可变](https://leetcode-cn.com/problems/range-sum-query-immutable/)

Difficulty: **简单**


给定一个整数数组  _nums_，求出数组从索引 _i _到 _j  _(_i_ ≤ _j_) 范围内元素的总和，包含 _i,  j _两点。

**示例：**

```
给定 nums = [-2, 0, 3, -5, 2, -1]，求和函数为 sumRange()

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
```

**说明:**

1.  你可以假设数组不可变。
2.  会多次调用 _sumRange_ 方法。


#### Solution1 - 暴力法

Language: **Java**
time:O(n) space:O(1)
```java
​private int[] data;

public NumArray(int[] nums) {
    data = nums;
}

public int sumRange(int i, int j) {
    int sum = 0;
    for (int k = i; k <= j; k++) {
        sum += data[k];
    }
    return sum;
}
```

#### Solution2 - 缓存

Language: **Java**
time:O(1) space:O(n^2)
```java
​private Map<Pair<Integer, Integer>, Integer> map = new HashMap<>();

public NumArray(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
        int sum = 0;
        for (int j = i; j < nums.length; j++) {
            sum += nums[j];
            map.put(Pair.create(i, j), sum);
        }
    }
}

public int sumRange(int i, int j) {
    return map.get(Pair.create(i, j));
}
```


#### Solution3 - 缓存优化

Language: **Java**
time:O(1) space:O(n)
```java
private int[] sum;

public NumArray(int[] nums) {
    sum = new int[nums.length + 1];
    for (int i = 0; i < nums.length; i++) {
        sum[i + 1] = sum[i] + nums[i];
    }
}

public int sumRange(int i, int j) {
    return sum[j + 1] - sum[i];
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/range-sum-query-immutable/solution/qu-yu-he-jian-suo-shu-zu-bu-ke-bian-by-leetcode/)***
