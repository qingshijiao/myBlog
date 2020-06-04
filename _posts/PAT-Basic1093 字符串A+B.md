---
title: 1093 字符串A+B (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
给定两个字符串 AAA 和 BBB，本题要求你输出 A+BA+BA+B，即两个字符串的并集。要求先输出 AAA，再输出 BBB，但
**重复的字符必须被剔除** 。

### 输入格式：

输入在两行中分别给出 AAA 和 BBB，均为长度不超过 10610^610​6​​的、由可见 ASCII 字符
(即码值为32~126)和空格组成的、由回车标识结束的非空字符串。

### 输出格式：

在一行中输出题面要求的 AAA 和 BBB 的和。

### 输入样例：

    
    
    This is a sample test
    to show you_How it works
    

### 输出样例：

    
    
    This ampletowyu_Hrk
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <set>
using namespace std;
int main() {
    string a, b;
    getline(cin, a);
    getline(cin, b);
    set<char> s;
    for (int i = 0; i < a.length(); ++i) {
        if (s.count(a[i]) == 0) {
            printf("%c", a[i]);
            s.insert(a[i]);
        }
    }
    for (int i = 0; i < b.length(); ++i) {
        if (s.count(b[i]) == 0) {
            printf("%c", b[i]);
            s.insert(b[i]);
        }
    }
}
```

```c++
#include <iostream>
using namespace std;
int main() {
    string s1, s2, s;
    int hash[200] = {0};
    getline(cin, s1);
    getline(cin, s2);
    s = s1 + s2;
    for (int i = 0; i < s.size(); i++) {
        if (hash[s[i]] == 0) cout << s[i];
        hash[s[i]] = 1;
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/1071785884776722432)***
