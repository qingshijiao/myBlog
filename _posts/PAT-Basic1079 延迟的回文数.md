---
title: 1079 延迟的回文数 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
给定一个 k+1 位的正整数 N，写成 ak⋯a1a0 的形式，其中对所有 iii 有 0≤ai<100  且 ak>0。N 被称为一个 **回文数** ，当且仅当对所有 i 有 a​i​​=a​k−i​​。零也被定义为一个回文数。

非回文数也可以通过一系列操作变出回文数。首先将该数字逆转，再将逆转数与该数相加，如果和还不是一个回文数，就重复这个逆转再相加的操作，直到一个回文数出现。如果一个非回文数可以变出回文数，就称这个数为
**延迟的回文数** 。（定义翻译自 <https://en.wikipedia.org/wiki/Palindromic_number> ）

给定任意一个正整数，本题要求你找到其变出的那个回文数。

### 输入格式：

输入在一行中给出一个不超过1000位的正整数。

### 输出格式：

对给定的整数，一行一行输出其变出回文数的过程。每行格式如下

    
    
    A + B = C
    

其中 `A` 是原始的数字，`B` 是 `A` 的逆转数，`C` 是它们的和。`A` 从输入的整数开始。重复操作直到 `C` 在 10
步以内变成回文数，这时在一行中输出 `C is a palindromic number.`；或者如果 10 步都没能得到回文数，最后就在一行中输出
`Not found in 10 iterations.`。

### 输入样例 1：

    
    
    97152
    

### 输出样例 1：

    
    
    97152 + 25179 = 122331
    122331 + 133221 = 255552
    255552 is a palindromic number.
    

### 输入样例 2：

    
    
    196
    

### 输出样例 2：

    
    
    196 + 691 = 887
    887 + 788 = 1675
    1675 + 5761 = 7436
    7436 + 6347 = 13783
    13783 + 38731 = 52514
    52514 + 41525 = 94039
    94039 + 93049 = 187088
    187088 + 880781 = 1067869
    1067869 + 9687601 = 10755470
    10755470 + 07455701 = 18211171
    Not found in 10 iterations.
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <algorithm>
using namespace std;
string rev(string s) {
    reverse(s.begin(), s.end());
    return s;
}
string add(string s1, string s2) {
    string s = s1;
    int carry = 0;
    for (int i = s1.size() - 1; i >= 0; i--) {
        s[i] = (s1[i] - '0' + s2[i] - '0' + carry) % 10 + '0';
        carry = (s1[i] - '0' + s2[i] - '0' + carry) / 10;
    }
    if (carry > 0) s = "1" + s;
    return s;
}
int main() {
    string s, sum;
    int n = 10;
    cin >> s;
    if (s == rev(s)) {
        cout << s << " is a palindromic number.\n";
        return 0;
    }
    while (n--) {
        sum = add(s, rev(s));
        cout << s << " + " << rev(s) << " = " << sum << endl;
        if (sum == rev(sum)) {
            cout << sum << " is a palindromic number.\n";
            return 0;
        }
        s = sum;
    }
    cout << "Not found in 10 iterations.\n";
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805261754023936)***
