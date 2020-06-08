---
title: 465. 最优账户平衡 (Optimal Account Balancing)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
## 题目
A group of friends went on holiday and sometimes lent each other money. For example, Alice paid for Bill's lunch for 10.ThenlaterChrisgaveAlice5 for a taxi ride. We can model each transaction as a tuple (x, y, z) which means person x gave person y $z. Assuming Alice, Bill, and Chris are person 0, 1, and 2 respectively (0, 1, 2 are the person's ID), the transactions can be represented as [[0, 1, 10], [2, 0, 5]].

Given a list of transactions between a group of people, return the minimum number of transactions required to settle the debt.

Note:

A transaction will be given as a tuple (x, y, z). Note that x ≠ y and z > 0.
Person's IDs may not be linear, e.g. we could have the persons 0, 1, 2 or we could also have the persons 0, 2, 6.
 

Example 1:

Input:
[[0,1,10], [2,0,5]]

Output:
2

Explanation:
Person #0 gave person #1 $10.
Person #2 gave person #0 $5.

Two transactions are needed. One way to settle the debt is person #1 pays person #0 and #2 $5 each.
 

Example 2:

Input:
[[0,1,10], [1,0,1], [1,2,5], [2,0,5]]

Output:
1

Explanation:
Person #0 gave person #1 $10.
Person #1 gave person #0 $1.
Person #1 gave person #2 $5.
Person #2 gave person #0 $5.

Therefore, person #1 only need to give person #0 $4, and all debt is settled.


#### Solution

Language: **c++**

```c++
class Solution {
public:
    int minTransfers(vector<vector<int>>& transactions) {
        int res = INT_MAX;
        unordered_map<int, int> m;
        for (auto t : transactions) {
            m[t[0]] -= t[2];
            m[t[1]] += t[2];
        }
        vector<int> accnt;
        for (auto a : m) {
            if (a.second != 0) accnt.push_back(a.second);
        }
        helper(accnt, 0, 0, res);
        return res;
    }
    void helper(vector<int>& accnt, int start, int cnt, int& res) {
        int n = accnt.size();
        while (start < n && accnt[start] == 0) ++start;
        if (start == n) {
            res = min(res, cnt);
            return;
        }
        for (int i = start + 1; i < n; ++i) {
            if ((accnt[i] < 0 && accnt[start] > 0) || (accnt[i] > 0 && accnt[start] < 0)) {
                accnt[i] += accnt[start];
                helper(accnt, start + 1, cnt + 1, res);
                accnt[i] -= accnt[start];
            }
        }
    }
};
```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/6108158.html)***
