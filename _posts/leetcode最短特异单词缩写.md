---
title: 411. 最短特异单词缩写 (Minimum Unique Word Abbreviation)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
A string such as "word" contains the following abbreviations:

["word", "1ord", "w1rd", "wo1d", "wor1", "2rd", "w2d", "wo2", "1o1d", "1or1", "w1r1", "1o2", "2r1", "3d", "w3", "4"]
Given a target string and a set of strings in a dictionary, find an abbreviation of this target string with thesmallest possible length such that it does not conflict with abbreviations of the strings in the dictionary.

Each number or letter in the abbreviation is considered length = 1. For example, the abbreviation "a32bc" has length = 4.

**Note:**

In the case of multiple answers as shown in the second example below, you may return any one of them.
Assume length of target string = m, and dictionary size = n. You may assume that m ≤ 21, n ≤ 1000, and log2(n) + m ≤ 20.
 

Examples:
```
"apple", ["blade"] -> "a4" (because "5" or "4e" conflicts with "blade")

"apple", ["plain", "amber", "blade"] -> "1p3" (other valid answers include "ap3", "a3e", "2p2", "3le", "3l1").
```


#### Solution

Language: **c++**

```c++
class Solution {
public:
    string minAbbreviation(string target, vector<string>& dictionary) {
        if (dictionary.empty()) return to_string((int)target.size());
        priority_queue<pair<int, string>, vector<pair<int, string>>, greater<pair<int, string>>> q;
        q = generate(target);
        while (!q.empty()) {
            auto t = q.top(); q.pop();
            bool no_conflict = true;
            for (string word : dictionary) {
                if (valid(word, t.second)) {
                    no_conflict = false;
                    break;
                }
            }
            if (no_conflict) return t.second;
        }
        return "";
    }
    priority_queue<pair<int, string>, vector<pair<int, string>>, greater<pair<int, string>>> generate(string target) {
        priority_queue<pair<int, string>, vector<pair<int, string>>, greater<pair<int, string>>> res;
        for (int i = 0; i < pow(2, target.size()); ++i) {
            string out = "";
            int cnt = 0, size = 0;
            for (int j = 0; j < target.size(); ++j) {
                if ((i >> j) & 1) ++cnt;
                else {
                    if (cnt != 0) {
                        out += to_string(cnt);
                        cnt = 0;
                        ++size;
                    }
                    out += target[j];
                    ++size;
                }
            }
            if (cnt > 0) {
                out += to_string(cnt);
                ++size;
            }
            res.push({size, out});
        }
        return res;
    }
    bool valid(string word, string abbr) {
        int m = word.size(), n = abbr.size(), p = 0, cnt = 0;
        for (int i = 0; i < abbr.size(); ++i) {
            if (abbr[i] >= '0' && abbr[i] <= '9') {
                if (cnt == 0 && abbr[i] == '0') return false;
                cnt = 10 * cnt + abbr[i] - '0';
            } else {
                p += cnt;
                if (p >= m || word[p++] != abbr[i]) return false;
                cnt = 0;
            }
        }
        return p + cnt == m;
    }
};
```

---
***参考：
[grandyang](https://www.cnblogs.com/grandyang/p/5935836.html)***
