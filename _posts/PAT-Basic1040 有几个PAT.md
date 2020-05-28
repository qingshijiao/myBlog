---
title: 1040 有几个PAT (25分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
字符串 `APPAPT` 中包含了两个单词 `PAT`，其中第一个 `PAT` 是第 2 位(`P`)，第 4 位(`A`)，第 6 位(`T`)；第二个
`PAT` 是第 3 位(`P`)，第 4 位(`A`)，第 6 位(`T`)。

现给定字符串，问一共可以形成多少个 `PAT`？

### 输入格式：

输入只有一行，包含一个字符串，长度不超过10510^510​5​​，只包含 `P`、`A`、`T` 三种字母。

### 输出格式：

在一行中输出给定字符串中包含多少个 `PAT`。由于结果可能比较大，只输出对 1000000007 取余数的结果。

### 输入样例：

    
    
    APPAPT
    

### 输出样例：

    
    
    2
    

#### Solution

Language: **C++**
```C++
#include <iostream>
using namespace std;
int main() {
    string s;
    cin >> s;
    int postT = 0, postA = 0, postP = 0, flagT = 0 , flagA = 0;
    for (int i = s.length() - 1; i >= 0; i--) {
        if (s[i] == 'T') {
            postT++;
            flagT = 1;
        }
        if (flagT == 1 && s[i] == 'A') {
            postA  = (postA + postT) % 1000000007;
            flagA = 1;
        }
        if (flagT == 1 && flagA == 1 && s[i] == 'P') {
            postP  = (postP + postA) % 1000000007;
        }
    }
    cout << postP;
    return 0;
}
```
```C++
#include <iostream>
#include <string>
using namespace std;
int main() {
    string s;
    cin >> s;
    int len = s.length(), result = 0, countp = 0, countt = 0;
    for (int i = 0; i < len; i++) {
        if (s[i] == 'T')
            countt++;
    }
    for (int i = 0; i < len; i++) {
        if (s[i] == 'P') countp++;
        if (s[i] == 'T') countt--;
        if (s[i] == 'A') result = (result + (countp * countt) % 1000000007) % 1000000007;
    }
    cout << result;
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805282389999616)***
