---
title: 1084 外观数列 (20分)
date: {{date}}
categories:
- PAT
tags:
- PAT
---
外观数列是指具有以下特点的整数序列：

    
    
    d, d1, d111, d113, d11231, d112213111, ...
    

它从不等于 1 的数字 `d` 开始，序列的第 n+1 项是对第 n 项的描述。比如第 2 项表示第 1 项有 1 个 `d`，所以就是 `d1`；第 2
项是 1 个 `d`（对应 `d1`）和 1 个 1（对应 11），所以第 3 项就是 `d111`。又比如第 4 项是 `d113`，其描述就是 1 个
`d`，2 个 1，1 个 3，所以下一项就是 `d11231`。当然这个定义对 `d` = 1 也成立。本题要求你推算任意给定数字 `d` 的外观数列的第
N 项。

### 输入格式：

输入第一行给出 [0,9] 范围内的一个整数 `d`、以及一个正整数 N（≤\le≤ 40），用空格分隔。

### 输出格式：

在一行中给出数字 `d` 的外观数列的第 N 项。

### 输入样例：

    
    
    1 8
    

### 输出样例：

    
    
    1123123111
    

#### Solution

Language: **C++**
```C++
#include <iostream>
#include <string>
using namespace std;
int main() {
    string d, temp;
    int n, cnt;
    cin >> d >> n;
    for (int i = 1; i < n; ++i) {
        temp = "";
        int len = d.length();
        if (len == 1) {
        	d += '1';
        	continue;
		}
        for (int j = 0; j < len - 1; ++j) {
        	cnt = 1;
            while (j < len - 1 && d[j] == d[j + 1]){
                ++cnt;
                ++j;
            }
            temp += d[j];
            temp += to_string(cnt);
        }
        if (d[len - 1] != d[len - 2]) {
            temp += d[len - 1];
            temp += '1';
        }
        d = temp;
    }
    cout << d;
    return 0;
}
```

**注意：+= 字符 效率比 = 高**

```c++
#include <iostream>
#include<string>
using namespace std;
string compress(string s, int n) {
	if (n == 1)		//直到n=1时，不需要压缩
		return s;
	string cs;		//压缩字符串
	int count = 1;
	for (int i = 0; i < s.length(); i++) {
		if (i < s.length() - 1 && s[i] == s[i + 1])	//与后一个进行比较
			count++;
		else {
			cs += s[i];
			cs += to_string(count);
			count = 1;
		}
	}
	s = cs;
	return compress(s, n - 1);		//递归再压缩一次
}
int main() {
	string str;
	int n;
	cin >> str >> n;
	cout << compress(str, n);;
	return 0;
}
```

```c++
#include <iostream>
using namespace std;
int main() {
    string s;
    int n, j;
    cin >> s >> n;
    for (int cnt = 1; cnt < n; cnt++) {
        string t;
        for (int i = 0; i < s.length(); i = j) {
            for (j = i; j < s.length() && s[j] == s[i]; j++);
            t += s[i] + to_string(j - i);
        }
        s = t;
    }
    cout << s;
    return 0;
}
```
---
***参考：
[pintia](https://pintia.cn/problem-sets/994805260223102976/problems/994805260583813120)***
