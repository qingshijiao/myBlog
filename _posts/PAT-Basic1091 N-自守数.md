---
title: 1091 N-自守数 (15分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
如果某个数 KKK 的平方乘以 N 以后，结果的末尾几位数等于 K，那么就称这个数为“N-自守数”。例如 3 × 92^2 = 25 392，而 25 392 的末尾两位正好是 92，所以 92 是一个
333-自守数。

本题就请你编写程序判断一个给定的数字是否关于某个 N 是 N-自守数。

### 输入格式：

输入在第一行中给出正整数 M（≤20），随后一行给出 M 个待检测的、不超过 1000 的正整数。

### 输出格式：

对每个需要检测的数字，如果它是 N-自守数就在一行中输出最小的 N 和 NK^2 的值，以一个空格隔开；否则输出
`No`。注意题目保证 N < 10。

### 输入样例：

    
    
    3
    92 5 233
    

### 输出样例：

    
    
    3 25392
    1 25
    No
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <cmath>
using namespace std;
int main() {
    int m, mt;
    scanf("%d", &m);
    for (int i = 0; i < m; ++i) {
        scanf("%d", &mt);
        int j, temp = pow(10, to_string(mt).length());
        for (j = 0; j < 10; ++j) {
            int sum = j * mt * mt;
            if (sum % temp == mt) {
                printf("%d %d\n", j, sum);
                break;
            }
        }
        if (j == 10) {
            printf("No\n");
        }
    }
	return 0;
}
```

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
    int m;
    cin >> m;
    while (m--) {
        int k, flag = 0;
        cin >> k;
        for (int n = 1; n < 10; n++) {
            int mul = n * k * k;
            string smul = to_string(mul), sk = to_string(k);
            string smulend = smul.substr(smul.length() - sk.length());
            if (smulend == sk) {
                printf("%d %d\n", n, mul);
                flag = 1;
                break;
            }
        }
        if (flag == 0) printf("No\n");
    }
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/1071785664454127616)***
