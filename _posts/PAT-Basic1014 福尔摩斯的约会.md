---
title: 1014 福尔摩斯的约会 (20分)

date: {{date}}
categories:
- PAT
tags:
- PAT

---
![image.png](https://i.loli.net/2020/05/23/tPDw6U2yOcgl9B8.png)

#### Solution

Language: **C++**

```C++
#include <iostream>
#include <ctype.h>

using namespace std;

int main() {
    string weeks[] = {"MON", "TUE", "WED", "THU", "FRI", "SAT", "SUN"};
    string s1 = "", s2 = "", s3 = "", s4 = "";
    int i = 0;
    cin >> s1 >> s2 >> s3 >> s4;
    for(; i < s1.length() && i < s2.length(); i++) {
        if(s1[i] == s2[i] && (s1[i] >= 'A' && s1[i] <= 'G')) {
            cout << weeks[s1[i] - 'A'] << " ";
            break;
        }
    }
    i++;
    for(; i < s1.length() && i < s2.length(); i++) {
        if(s1[i] == s2[i]) {
            if(isdigit(s1[i]) != 0){
                printf("%02d:", (s1[i] - '0'));
                break;
            }
            else if(s1[i] >= 'A' && s1[i] <= 'N') {
                cout << (s1[i] - 'A' + 10) << ":";
                break;
            }
        }
        
    }
    for(int j = 0; j < s3.length() && j < s4.length(); j++) {
        if(s3[j] == s4[j] && isalpha(s3[j]) != 0) {
            printf("%02d", j);
            break;
        }
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805308755394560)***
