---
title: 307.区域和检索 - 数组可修改(Range Sum Query - Mutable)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [307\. 区域和检索 - 数组可修改](https://leetcode-cn.com/problems/range-sum-query-mutable/)

Difficulty: **中等**


给定一个整数数组  _nums_，求出数组从索引 _i _到 _j  _(_i_ ≤ _j_) 范围内元素的总和，包含 _i,  j _两点。

_update(i, val)_ 函数可以通过将下标为 _i _的数值更新为 _val_，从而对数列进行修改。

**示例:**

```
Given nums = [1, 3, 5]

sumRange(0, 2) -> 9
update(1, 2)
sumRange(0, 2) -> 8
```

**说明:**

1.  数组仅可以在 _update _函数下进行修改。
2.  你可以假设 _update_ 函数与 _sumRange_ 函数的调用次数是均匀分布的。


#### Solution1 - 暴力

Language: **Java**
time:O(n) space:O(1)
```java
​private int[] nums;
public int sumRange(int i, int j) {
    int sum = 0;
    for (int l = i; l <= j; l++) {
        sum += data[l];
    }
    return sum;
}

public int update(int i, int val) {
    nums[i] = val;
}
```

#### Solution2 - sqrt 分解

![](https://pic.leetcode-cn.com/78228fc5dd4fc247edd104eed32351f25e449f858b67acf96845474981bbf451-file_1561890424409)

Language: **Java**

```java
​private int[] b;
private int len;
private int[] nums;

public NumArray(int[] nums) {
    this.nums = nums;
    double l = Math.sqrt(nums.length);
    len = (int) Math.ceil(nums.length/l);
    b = new int [len];
    for (int i = 0; i < nums.length; i++)
        b[i / len] += nums[i];
}

public int sumRange(int i, int j) {
    int sum = 0;
    int startBlock = i / len;
    int endBlock = j / len;
    if (startBlock == endBlock) {
        for (int k = i; k <= j; k++)
            sum += nums[k];
    } else {
        for (int k = i; k <= (startBlock + 1) * len - 1; k++)
            sum += nums[k];
        for (int k = startBlock + 1; k <= endBlock - 1; k++)
            sum += b[k];
        for (int k = endBlock * len; k <= j; k++)
            sum += nums[k];
    }
    return sum;
}

public void update(int i, int val) {
    int b_l = i / len;
    b[b_l] = b[b_l] - nums[i] + val;
    nums[i] = val;
}
// Accepted
```

#### Solution3 - 二叉索引树

![](https://pic.leetcode-cn.com/edd9a82516c480c3f245b5be34f740cad4c60d4e45d4bf29254333dd4f1806fe-file_1561890424409)

Language: **Java**

```java
​class NumArray {
    private final int[] nums;
    private final int[] arr;
    private final int len;

    public NumArray(int[] nums) {
        // use binary indexed tree to solve
        len = nums.length;

        this.nums = new int[len];

        arr = new int[len + 1];
        for (int i = 0; i < len; i++) {
            update(i, nums[i]);
        }
    }

    public void update(int i, int val) {
        updateBIT(convertIndex(i), val - nums[i]);
        nums[i] = val;
    }

    private void updateBIT(int i, int delta) {
        while (i <= len) {
            arr[i] += delta;
            i += lowbit(i);
        }
    }

    // count sum from [1, i]
    private int countSumBIT(int i) {
        int sum = 0;
        while (i > 0) {
            sum += arr[i];
            i -= lowbit(i);
        }
        return sum;
    }


    public int sumRange(int i, int j) {
        return countSumBIT(convertIndex(j)) - countSumBIT(convertIndex(i-1));
    }


    private int lowbit(int i) {
        return i & (-i);
    }

    private int convertIndex(int i) {
        return i + 1;
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * obj.update(i,val);
 * int param_2 = obj.sumRange(i,j);
 */
```

---
***参考：
[leetcode](https://leetcode-cn.com/problems/range-sum-query-mutable/solution/qu-yu-he-jian-suo-shu-zu-ke-xiu-gai-by-leetcode/)***
