---
title: 170.两数之和 III - 数据结构设计（Majority Element）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
设计b并实现一个 TwoSum 类。他需要支持以下操作:add 和 find。
add -把这个数添加到内部的数据结构。
find -是否存在任意一对数字之和等于这个值
样例
样例 1:
```
add(1);add(3);add(5);
find(4)//返回true
find(7)//返回false
```

# 题解

## 官方题解
暂无

## 其他题解
### 1.设计数据结构
**思路：**
```
public class TwoSum {
    private HashMap<Integer, Integer> elements = new HashMap<Integer, Integer>();

    public void add(int number) {
        if (elements.containsKey(number)) {
            elements.put(number, elements.get(number) + 1);
        } else {
            elements.put(number, 1);
        }
    }

    public boolean find(int value) {
        for (Integer i : elements.keySet()) {
            int target = value - i;
            if (elements.containsKey(target)) {
                if (i == target && elements.get(target) < 2) {
                    continue;
                }
                return true;
            }
        }
        return false;
    }
}
```

---
***参考：
[LeetCode](https://www.cnblogs.com/lightwindy/p/8481907.html)***
