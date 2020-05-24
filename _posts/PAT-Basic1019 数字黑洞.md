---
title: 1019 数字黑洞 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/VjxrqTbHIe3LMP5.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
#include <algorithm>
#include <string>
using namespace std;
bool cmp(char a, char b) {return a > b;}
int main() {
    string s;
    cin >> s;
    s.insert(0, 4 - s.length(), '0');
    do {
        string a = s, b = s;
        sort(a.begin(), a.end(), cmp);
        sort(b.begin(), b.end());
        int result = stoi(a) - stoi(b);
        s = to_string(result);
        s.insert(0, 4 - s.length(), '0');
        cout << a << " - " << b << " = " << s << endl;
    } while (s != "6174" && s != "0000");
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805302786899968)***
