---
title: 1087 有多少不同的值 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
当自然数 nnn 依次取 1、2、3、……、NNN 时，算式 ⌊n/2⌋+⌊n/3⌋+⌊n/5⌋\lfloor n/2\rfloor +\lfloor
n/3\rfloor +\lfloor n/5\rfloor ⌊n/2⌋+⌊n/3⌋+⌊n/5⌋ 有多少个不同的值？（注：⌊x⌋\lfloor
x\rfloor⌊x⌋ 为取整函数，表示不超过 xxx 的最大自然数，即 xxx 的整数部分。）

### 输入格式：

输入给出一个正整数 NNN（2≤N≤1042 \le N \le 10^42≤N≤10​4​​）。

### 输出格式：

在一行中输出题面中算式取到的不同值的个数。

### 输入样例：

    
    
    2017
    

### 输出样例：

    
    
    1480
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <set>
using namespace std;
int main() {
	int n, cnt = 0;
    scanf("%d", &n);
    set<int> sett;
    for (int i = 1; i <= n; ++i) {
        sett.insert(i / 2 + i / 3 + i / 5);
    }
    printf("%d", sett.size());
	return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/1038429191091781632)***
