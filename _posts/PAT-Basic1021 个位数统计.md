---
title: 1021 个位数统计 (15分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/24/5sfDhNnC9RtcHvJ.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
using namespace std;
int main() {
    string s;
    cin >> s;
    int a[10] = {0};
    for (int i = 0; i < s.length(); i++)
        a[s[i] - '0']++;
    for (int i = 0; i < 10; i++) {
        if (a[i] != 0) 
            printf("%d:%d\n", i, a[i]);
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805300404535296)***
