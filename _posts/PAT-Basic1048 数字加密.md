---
title: 1048 数字加密 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
本题要求实现一种数字加密方法。首先固定一个加密用正整数 A，对任一正整数 B，将其每 1 位数字与 A
的对应位置上的数字进行以下运算：对奇数位，对应位的数字相加后对 13 取余——这里用 J 代表 10、Q 代表 11、K 代表 12；对偶数位，用 B
的数字减去 A 的数字，若结果为负数，则再加 10。这里令个位为第 1 位。

### 输入格式：

输入在一行中依次给出 A 和 B，均为不超过 100 位的正整数，其间以空格分隔。

### 输出格式：

在一行中输出加密后的结果。

### 输入样例：

    
    
    1234567 368782971
    

### 输出样例：

    
    
    3695Q8118
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    string s1, s2;
    cin >> s1 >> s2;
    char str[14] = {"0123456789JQK"};
    int len1 = s1.length(), len2 = s2.length();
    string temp = "";
    for(int i = 0; i < abs(len1 - len2); i++) {
        temp +='0';
    }
    if(len1 < len2) {
        s1 = temp + s1;
    } else if (len1 > len2) {
        s2 = temp + s2;
    }
    int len = s2.length();
    for (int i = 0; i < len; i++) {
        int j = len - 1 - i;
        if (i % 2 == 0) {
            s2[j] = str[(s1[j] - '0' + s2[j] - '0') % 13];
        } else {
            int r = s2[j] - s1[j];
            if (r < 0) r += 10;
            s2[j] = str[r];
        }
    }
    cout << s2;
    return 0;
}
```

```c++
#include <iostream>
#include <algorithm>
using namespace std;
int main() {
    string a, b, c;
    cin >> a >> b;
    int lena = a.length(), lenb = b.length();
    reverse(a.begin(), a.end());
    reverse(b.begin(), b.end());
    if (lena > lenb) 
        b.append(lena - lenb, '0');
    else
        a.append(lenb - lena, '0');
    char str[14] = {"0123456789JQK"};
    for (int i = 0; i < a.length(); i++) {
        if (i % 2 == 0) {
            c += str[(a[i] - '0' + b[i] - '0') % 13];
        } else {
            int temp = b[i] - a[i];
            if (temp < 0) temp = temp + 10;
            c += str[temp];
        }
    }
    for (int i = c.length() - 1; i >= 0; i--)
        cout << c[i];
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805276438282240)***
