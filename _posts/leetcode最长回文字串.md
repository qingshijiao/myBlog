---
title: 5.最长回文字串(Longest Palindromic Substring)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

示例 1：
> 输入: "babad"
> 输出: "bab"
> 注意: "aba" 也是一个有效答案。

示例 2：
> 输入: "cbbd"
> 输出: "bb"


# 题解

## 官方题解
官方有的没代码，我整理在其他题解中了，方法都一样。


## 其他题解
### 1.暴力法
**思想：** 暴力求解，列举所有的字串，判断是否为回文串，保存最长的回文串
```
//判断是否为回文串
public boolean isPalindromic(String s) {
    int len = s.length();
    for (int i = 0; i < len / 2; i++) {
      if (s.charAt(i) != s.charAt(len - i - 1)) {
        return false;
      }
    }
    return true;
}

// 暴力解法
public String longestPalindrome(String s) {
    String ans = "";
    int max = 0;
    int len = s.length();
    for (int i = 0; i < len; i++)
        for (int j = i + 1; j <= len; j++) {
            String test = s.substring(i, j);
            if (isPalindromic(test) && test.length() > max) {
                ans = s.substring(i, j);
                max = Math.max(max, ans.length());
            }
        }
    return ans;
}
```
> 复杂度分析
>
> - 时间复杂度：O(n^3)
> - 空间复杂度：O(1)

### 2.暴力法优化（动态规划）
**思想：** 我们构建一个公式 **P(i,j)=(P(i+1,j−1)&&S[i]==S[j])** ，类似递推。

意思是我们如果知道一个字符串是回文，那么在它两端各添加一个字母后，我们只需要判断新添加的字母是否相等就可以知道新字符串是否为回文串。（比如a和bac，bb和abbc）
由于i，j分别表示字符串的开头和结尾，所以 i <= j , 有效区为有颜色部分，箭头为递推方向。（比如我们想知道 s[0, 5] 字符串的回文性质, 我们只需知道 s[1, 4] && s[0] == s[5], 再递推即要知道 s[2, 3] && s[1] == s[4]）
![](https://i.loli.net/2019/08/11/radbx4Wsk2zMuDy.png)
由于我们要想知道 P(i,j)，必须要知道 P(i+1,j−1) 是否为回文，所以我们可以反向遍历。（如果正向遍历就需要用递归）
方向遍历顺序如下，这样我们要求第 4 个，我们就需要知道第 3 个，第 3 个已经求过了。我们可以利用二维矩阵来存储数据，我们也可以用一维矩阵存储。

一维矩阵怎么储存呢，我们可以发现当我们遍历到第 7 个时，我们第 1、2、3 个数据是不再使用了，但是仍然占据着空间，所以我们只保留前一行。当遍历到第 11 个时，由于我们保留了第 8 个字符串，就可以不必非得递归到第 6 个再去判断。
![](https://i.loli.net/2019/08/11/cxPX7fb4QSKZd82.png)

```
public String longestPalindrome7(String s) {
    int n = s.length();
    String res = "";
    boolean[] P = new boolean[n];
    for (int i = n - 1; i >= 0; i--) {
        for (int j = n - 1; j >= i; j--) {
            //不需要进行递归判断的字符串长度小于 3
            //由于保留的是前一行，所以 p[j - 1] 就可以表示左对角
            P[j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || P[j - 1]);
            if (P[j] && j - i + 1 > res.length()) {
              res = s.substring(i, j + 1);
            }
        }
    }
      return res;
}
```
> 复杂度分析
>
> - 时间复杂度：O(n^2)
> - 空间复杂度：O(n)

### 3.最长公共字串（动态规划）
**思想：** 将字符串翻转寻找最长公共字串。这次是从左上向右下观察。
实际上是拿原字符串的字符与翻转字符串进行配对，标记可能是最长字串的位置。
![](https://i.loli.net/2019/08/11/HMWKvz1NYjg9oPy.png)
对于第一列，我们拿 a 配对，标记了初始位置。第二列，当配对到 b 时，由于它前一个字符配对成功(A[3, 0] 位置), 所以我们要在其基础上加 1 .
![](https://i.loli.net/2019/08/11/wWCqmeUaudZSG9Q.png)
可以用二维矩阵存储，也可以利用一维矩阵存储前一列的数据（由于使用的是左上角的数据，从 0 开始遍历会覆盖原来的数据，所以使用倒序遍历）。
*易错点：我们找的是最长字串，但不代表它一定是回文（abcdfgcba 和 翻转后 abcgfdabc 最长字串 abc 不是回文）。只需要判断字符串的首尾字符是否相等即可*

```
public String longestPalindrome(String s) {
    if (s.equals(""))
        return "";
    String origin = s;
    String reverse = new StringBuffer(s).reverse().toString();
    int length = s.length();
    int[] arr = new int[length];
    int maxLen = 0;
    int maxEnd = 0;
    for (int i = 0; i < length; i++)
        for (int j = length - 1; j >= 0; j--) {
            if (origin.charAt(i) == reverse.charAt(j)) {
                if (i == 0 || j == 0) {
                    arr[j] = 1;
                } else {
                    arr[j] = arr[j - 1] + 1;
                }
            //之前二维数组，每次用的是不同的列，所以不用置 0 。
            } else {
                arr[j] = 0;
            }
            if (arr[j] > maxLen) {
                //翻转前位置
                int beforeRev = length - 1 - j;
                //只判断字符串的首尾两个字符是否相等即可
                if (beforeRev + arr[j] - 1 == i) {
                    maxLen = arr[j];
                    maxEnd = i;
                }

            }
        }
    return s.substring(maxEnd - maxLen + 1, maxEnd + 1);
}
```
> 复杂度分析
>
> - 时间复杂度：O(n^2)
> - 空间复杂度：O(n)

### 4.中心扩展法
**思想：** 由于回文串一定是对称的，那么就有一个对称中心。每次循环选择一个中心，进行左右扩展，判断左右字符是否相等即可。
![](https://pic.leetcode-cn.com/1b9bfe346a4a9a5718b08149be11236a6db61b3922265d34f22632d4687aa0a8-image.png)
由于存在奇数的字符串和偶数的字符串，所以我们需要从一个字符开始扩展，或者从两个字符之间开始扩展，所以总共有 n+n-1 个中心。
```
public String longestPalindrome(String s) {
    if (s == null || s.length() < 1) return "";
    int start = 0, end = 0;
    for (int i = 0; i < s.length(); i++) {
        //单字符扩展
        int len1 = expandAroundCenter(s, i, i);
        //双字符扩展
        int len2 = expandAroundCenter(s, i, i + 1);
        int len = Math.max(len1, len2);
        if (len > end - start) {
            start = i - (len - 1) / 2;
            end = i + len / 2;
        }
    }
    return s.substring(start, end + 1);
}

private int expandAroundCenter(String s, int left, int right) {
    int L = left, R = right;
    while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R)) {
        L--;
        R++;
    }
    return R - L - 1;
}
```
> 复杂度分析
>
> - 时间复杂度：O(n^2)
> - 空间复杂度：O(1)

### 5.Manacher's Algorithm 马拉车算法
**思想：** 中心扩展的升级版。
> **问：** 为什么说是中心扩展法的升级版，优点在哪里?
> **答：** 有两个优点，一是将奇偶字符串统一了算法，二是利用回文串的性质减少了重复的运算。

#### 1) 统一奇偶字符串
我们可以将每个字符串字符间加上 #， 这样所有字符串都将变成奇数字符串。(abcd 变成 #a#b#c#d#)
还有一个问题是数组越界，为了不考虑数组越界等复杂条件，我们可以间字符串首尾再加上一个特殊字符，这样使用中心扩展法时，只要这两个字符和其它字符都不相同，会自动退出。(#a#b#c#d# 变成 ^#a#b#c#d#$, 这两个字符一般不会出现在字符串中)
#### 2) 利用回文串性质
我们知道回文串是关于中心对称的，我们对下面的字符串使用中心扩展法进行计算，将其为中心而形成的最大长度回文串记录在下方。
![](https://i.loli.net/2019/08/12/dt8Hvb5DswA1GIW.png)
这里使用 i = 4 为中心（i = 2，3也可以，这里为了更清晰说明效果），由于回文串是对称的，那么 i = 10 所能形成的最长回文串一定和 i = 6 相同，即 p[10] = 5。**这样我们就不必重新计算，直接使用已知数据就可以。**
![](https://i.loli.net/2019/08/12/Jt2nWNfCis4S5AT.png)
![](https://i.loli.net/2019/08/12/gIWDUAfLZa3THdi.png)
当我们遍历到 i = 12 时，会发现使用我们使用扩展法会超出以 i=8 为中心的回文串右边界，这时我们需要**更新右边界以便能继续使用回文串性质**。右边界 right = 16。
> **问：** 开始 right = 0，遍历时是什么情况？
> **答：** 从 i = 1 开始遍历到 i = 23, 开始 right = 0 < i = 1, 我们赋值 p[1] = 0, 此时由于 right < i + p[1]，right 是需要更新的，right = 1 + p[1] = 1，我们还记录了回文串中心 mid = i。（对于短回文串右边界更新比较频繁。）

```
// 马拉车算法
public String longestPalindrome(String s) {
    //改造字符串
    String t = preProcess(s);
    int n = t.length();
    //回文串长度数组
    int[] p = new int[n];
    //mi为最大回文串对应的中心点，right为该回文串能达到的最右端的值
    int mid = 0, right = 0;
    //maxLen为最大回文串的长度，maxPoint为记录中心点
    int maxLen=0, maxPoint=0;
    for(int i = 1; i < n - 1; ++i) {
        //对于某个 mid，其 right 固定
        if (right > i){
            //在边界内
            p[i] = Math.min(p[2 * mid - i], right - i);
        } else {
            p[i] = 0;
        }
        //循环递增条件是 p[i] 的增加，类似中心扩展
        //这里把回文串长度的增加记录在 p[i] 中，当扩展到字符不相等时退出
        //这里加减 1 表示不比较自身字符，# 不影响
        while(t.charAt(i + p[i] + 1) == t.charAt(i - p[i] - 1)){
            ++p[i];
        }
        //超过之前的最右端，则改变中心点和对应的最右端
        if(right < i + p[i]) {
            right = i + p[i];
            mid = i;
        }
        //更新最大回文串的长度，并记下此时的点
        if(maxLen < p[i]) {
            maxLen = p[i];
            maxPoint = i;
        }
    }
    return s.substring((maxPoint - maxLen) / 2, (maxPoint + maxLen) / 2);
}

public String preProcess(String s) {
    int n = s.length();
    if (n == 0) {
        return "^$";
    }
    String res = "^";
    for (int i = 0; i < n; i++){
        res += "#" + s.charAt(i);
    }
    res += "#$";
    return res;
}
```

> 复杂度分析
>
> - 时间复杂度：O(n)
> - 空间复杂度：O(n)

---
***参考：
[领扣](https://leetcode-cn.com/problems/two-sum/solution/liang-shu-zhi-he-by-leetcode-2/)
[windliang](https://leetcode-cn.com/problems/two-sum/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-bao-gu/)***
