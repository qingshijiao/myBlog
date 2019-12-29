---
title: 254.因子的组合（Meeting Rooms II）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Numbers can be regarded as product of its factors. For example,
```
8 = 2 x 2 x 2;
  = 2 x 4.

```
Write a function that takes an integer n and return all possible combinations of its factors.

Note:

- You may assume that n is always positive.
- Factors should be greater than 1 and less than n.

Example 1:
```
Input: 1
Output: []
```
Example 2:
```
Input: 37
Output:[]
```
Example 3:
```
Input: 12
Output:
[
  [2, 6],
  [2, 2, 3],
  [3, 4]
]
```
Example 4:
```
Input: 32
Output:
[
  [2, 16],
  [2, 2, 8],
  [2, 2, 2, 4],
  [2, 2, 2, 2, 2],
  [2, 4, 4],
  [4, 8]
]
```


#### Solution - 回溯

Language: **Java**

```java
public class Solution {
    public List<List<Integer>> getFactors(int n) {
        List<List<Integer>> res =  new ArrayList<>();
        if (n <= 1) return res;
        getFactors(res, new ArrayList<>(), n, 2);
        return res;
    }

    private void getFactors(List<List<Integer>> res, List<Integer> list, int n, int pos) {
        for (int i = pos; i <= Math.sqrt(n); i++) {
            if (n % i == 0 && n / i >= i) {
                list.add(i);
                list.add(n / i);
                res.add(new ArrayList<>(list));
                list.remove(list.size() - 1);
                getFactors(res, list, n / i, i);
                list.remove(list.size() - 1);
            }
        }
    }
}
```

---
***参考：
[YRB](https://www.cnblogs.com/yrbbest/p/5014873.html)***
