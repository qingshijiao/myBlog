---
title: 1042 字符统计 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
请编写程序，找出一段给定文字中出现最频繁的那个英文字母。

### 输入格式：

输入在一行中给出一个长度不超过 1000 的字符串。字符串由 ASCII 码表中任意可见字符及空格组成，至少包含 1
个英文字母，以回车结束（回车不算在内）。

### 输出格式：

在一行中输出出现频率最高的那个英文字母及其出现次数，其间以空格分隔。如果有并列，则输出按字母序最小的那个字母。统计时不区分大小写，输出小写字母。

### 输入样例：

    
    
    This is a simple TEST.  There ARE numbers and other symbols 1&2&3...........
    

### 输出样例：

    
    
    e 7
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <cctype>
using namespace std;
int main() {
    string text;
    getline(cin, text);
    int num[26] = {0}, max = 0;
    for (int i = 0; i < text.length(); i++) {
        if (isalpha(text[i])) {
            int index = tolower(text[i]) - 'a';
            num[index]++;
            if (num[index] > num[max]) {
                max = index;
            } else if (num[index] == num[max]) {
                max = max < index ? max: index;
            }
        }
    }
    printf("%c %d", max + 'a', num[max]);
    return 0;
}
```

```c++
#include <iostream>
#include <cctype>
#include <string>
using namespace std;
int main() {
    string s;
    getline(cin, s);
    int a[26] = {0};
    for (int i = 0; i < s.length(); i++)
        s[i] = tolower(s[i]);
    for (int i = 0; i < s.length(); i++)
        if (islower(s[i])) a[s[i] - 'a']++;
    int max = a[0], t = 0;
    for (int i = 1; i < 26; i++) {
        if (a[i] > max) {
            max = a[i];
            t = i;
        }
    }
    printf("%c %d", t + 'a', max);
    return 0;
}
```

注意：c++中string类怎么用scanf读取
```c++
#include <stdio.h>
#include <string>
using namespace std;
int main()
{
	string a;
	a.resize(100); //需要预先分配空间
	scanf("%s", &a[0]);
	puts(a.c_str());
	return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805280817135616)***
