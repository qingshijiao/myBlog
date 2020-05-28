---
title: 444.序列重建 (Sequence Reconstruction)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
Check whether the original sequence org can be uniquely reconstructed from the sequences in seqs. The org sequence is a permutation of the integers from 1 to n, with 1 ≤ n ≤ 104. Reconstruction means building a shortest common supersequence of the sequences in seqs (i.e., a shortest sequence so that all sequences in seqs are subsequences of it). Determine whether there is only one sequence that can be reconstructed from seqs and it is the org sequence.

Example 1:

Input:
org: [1,2,3], seqs: [[1,2],[1,3]]

Output:
false

Explanation:
[1,2,3] is not the only one sequence that can be reconstructed, because [1,3,2] is also a valid sequence that can be reconstructed.
Example 2:

Input:
org: [1,2,3], seqs: [[1,2]]

Output:
false

Explanation:
The reconstructed sequence can only be [1,2].
Example 3:

Input:
org: [1,2,3], seqs: [[1,2],[1,3],[2,3]]

Output:
true

Explanation:
The sequences [1,2], [1,3], and [2,3] can uniquely reconstruct the original sequence [1,2,3].
Example 4:

Input:
org: [4,1,5,2,6,3], seqs: [[5,2,6,3],[4,1,5,2]]

Output:
true




#### Solution

Language: **Java**

```java
​class Solution {
public:
    bool sequenceReconstruction(vector<int>& org, vector<vector<int>>& seqs) {
        if (seqs.empty()) return false;
        int n = org.size(), cnt = n - 1;
        vector<int> pos(n + 1, 0), flags(n + 1, 0);
        bool existed = false;
        for (int i = 0; i < n; ++i) pos[org[i]] = i;
        for (auto& seq : seqs) {
            for (int i = 0; i < seq.size(); ++i) {
                existed = true;
                if (seq[i] <= 0 || seq[i] > n) return false;
                if (i == 0) continue;
                int pre = seq[i - 1], cur = seq[i];
                if (pos[pre] >= pos[cur]) return false;
                if (flags[cur] == 0 && pos[pre] + 1 == pos[cur]) {
                    flags[cur] = 1; --cnt;
                }
            }
        }
        return cnt == 0 && existed;
    }
};
```

---
***参考:
[leetcode](https://www.cnblogs.com/grandyang/p/6032498.html)***
