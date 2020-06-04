---
title: 1086 就不告诉你 (15分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
做作业的时候，邻座的小盆友问你：“五乘以七等于多少？”你应该不失礼貌地围笑着告诉他：“五十三。”本题就要求你，对任何一对给定的正整数，倒着输出它们的乘积。

![53.jpg](https://images.ptausercontent.com/0c3a4497-27c3-45ea-9c8e-5a1ab2df48af.jpg)

### 输入格式：

输入在第一行给出两个不超过 1000 的正整数 A 和 B，其间以空格分隔。

### 输出格式：

在一行中倒着输出 A 和 B 的乘积。

### 输入样例：

    
    
    5 7
    

### 输出样例：

    
    
    53
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;
int main() {
	int n1, n2;
    scanf("%d%d", &n1, &n2);
    string res = to_string(n1 * n2);
    reverse(res.begin(), res.end());
    printf("%d", stoi(res));
	return 0;
}
```

**注意：开头要忽略 0**
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/1038429065476579328)***
