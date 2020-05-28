---
title: 1043 输出PATest (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
给定一个长度不超过 10410^410​4​​ 的、仅由英文字母构成的字符串。请将字符重新调整顺序，按 `PATestPATest....`
这样的顺序输出，并忽略其它字符。当然，六种字符的个数不一定是一样多的，若某种字符已经输出完，则余下的字符仍按 PATest
的顺序打印，直到所有字符都被输出。

### 输入格式：

输入在一行中给出一个长度不超过 10410^410​4​​ 的、仅由英文字母构成的非空字符串。

### 输出格式：

在一行中按题目要求输出排序后的字符串。题目保证输出非空。

### 输入样例：

    
    
    redlesPayBestPATTopTeePHPereatitAPPT
    

### 输出样例：

    
    
    PATestPATestPTetPTePePee
    

#### Solution

Language: **C++**
```C++
#include <iostream>
using namespace std;
int main() {
    string text;
    getline(cin, text);
    int n[6] = {0}, num = 0;
    char a[6] = {'P', 'A', 'T', 'e', 's', 't'};
    for (int i = 0; i < text.length(); i++) {
        for (int j = 0; j < 6; j++) {
            if (text[i] == a[j]) {
                n[j]++;
                break;
            }
        }
        num++;
    }
    for (int i = 0; i < num; i++) {
        for(int j = 0; j < 6; j++){
        	if (n[j] > 0) {
        		printf("%c", a[j]);
			}
            n[j]--;
        }
    }
    return 0;
}
```

```C++
#include <iostream>
using namespace std;
int main() {
  int map[128] = {0}, c;
  while ((c = cin.get()) != EOF) map[c]++;
  while (map['P'] > 0 || map['A'] > 0 || map['T'] > 0 || map['e'] > 0 || map['s'] > 0 || map['t'] > 0) {
    if (map['P']-- > 0) cout << 'P';
    if (map['A']-- > 0) cout << 'A';
    if (map['T']-- > 0) cout << 'T';
    if (map['e']-- > 0) cout << 'e';
    if (map['s']-- > 0) cout << 's';
    if (map['t']-- > 0) cout << 't';
  }
  return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805280074743808)***
