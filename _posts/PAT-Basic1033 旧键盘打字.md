---
title: 1033 旧键盘打字 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
旧键盘上坏了几个键，于是在敲一段文字的时候，对应的字符就不会出现。现在给出应该输入的一段文字、以及坏掉的那些键，打出的结果文字会是怎样？

### 输入格式：

输入在 2 行中分别给出坏掉的那些键、以及应该输入的文字。其中对应英文字母的坏键以大写给出；每段文字是不超过 10510^510​5​​
个字符的串。可用的字符包括字母 [`a`-`z`, `A`-`Z`]、数字 `0`-`9`、以及下划线
`_`（代表空格）、`,`、`.`、`-`、`+`（代表上档键）。题目保证第 2 行输入的文字串非空。

注意：如果上档键坏掉了，那么大写的英文字母无法被打出。

### 输出格式：

在一行中输出能够被打出的结果文字。如果没有一个字符能被打出，则输出空行。

### 输入样例：

    
    
    7+IE.
    7_This_is_a_test.
    

### 输出样例：

    
    
    _hs_s_a_tst
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <cctype>
using namespace std;
int main() {
    string s1, s2;
//     cin >> s1 >> s2;
//  cin无法读取空格
    getline(cin, s1);
    getline(cin, s2);
    bool canA = s1.find('+')  == string::npos;
    for (int i = 0; i < s2.length(); i++) {
        if (s1.find(toupper(s2[i])) == string::npos){
            if (!canA && (s2[i] >= 'A' && s2[i] <= 'Z')) {
                continue;
            }
            cout << s2[i];
        }
    }
    return 0;
}
```

---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805288530460672)***
