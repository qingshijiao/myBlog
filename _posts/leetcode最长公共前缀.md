---
title: 14.最长公共前缀（Longest Common Prefix）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 ""。

示例 1:
> 输入: ["flower","flow","flight"]
> 输出: "fl"

示例 2:
> 输入: ["dog","racecar","car"]
> 输出: ""
> 解释: 输入不存在公共前缀。


**说明:**
所有输入只包含小写字母 a-z 。

# 题解

## 官方题解
### 1.水平扫描法
**思路：** 由于是所有字符串的公共前缀，我们可以相比较前两个字符串的公共前缀，将结果再与第三个字符串比较，得到另一个结果···
最后得到的字符串就是所有字符串的公共前缀。
LSP(S1~Sn) = LCP(LCP(LCP(S1, S2), S3), ~Sn)

![](https://pic.leetcode-cn.com/b647cab7c3d2bd157cecae10917e0b9b671756b92c9cfcefec1a2bdae299c11c-file_1555694071243)

```
public String longestCommonPrefix(String[] strs) {
   if (strs.length == 0) return "";
   String prefix = strs[0];
   for (int i = 1; i < strs.length; i++){
     //查找后一个字符串是否包含前缀
     while (strs[i].indexOf(prefix) != 0) {
         prefix = prefix.substring(0, prefix.length() - 1);
         if (prefix.isEmpty()) return "";
     }
   }
   return prefix;
}
```

> **复杂度分析**
> - 时间复杂度：O(S), S 是所有字符串中字符数量的总和。
> 最坏的情况下，n 个字符串都是相同的。算法会将 S1 与其他字符串 [S2 ~ SN] 都做一次比较。这样就会进行 S 次字符比较，其中 S 是输入数据中所有字符数量。
> - 空间复杂度：O(1)

### 2.水平扫描法
**思想：** 比较不同字符串的相同下标位置（字符串 ab abc abcd 先将 ab 中 a 和其它字符串相同下标位置 a 比较判断是否相同，超出长度或者不同退出）

```
public String longestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0) return "";
    for (int i = 0; i < strs[0].length() ; i++){
        char c = strs[0].charAt(i);
        for (int j = 1; j < strs.length; j ++) {
            if (i == strs[j].length() || strs[j].charAt(i) != c)
                return strs[0].substring(0, i);
        }
    }
    return strs[0];
}
```

> **复杂度分析**
> - 时间复杂度：O(S), S 是所有字符串中字符数量的总和。
> 最坏情况下，输入数据为 n 个长度为 m 的相同字符串，算法会进行 S = m * n 次比较。可以看到最坏情况下，本算法的效率与算法一相同，但是最好的情况下，算法只需要进行 n * minLen 次比较，其中 minLen 是数组中最短字符串的长度。
> - 空间复杂度：O(1)

### 3.分治算法
**思想：** 将字符串数目划分成两部分，在进行计算。
![](https://pic.leetcode-cn.com/8bb79902c99719a923d835b9265b2dea6f20fe7f067f313cddcf9dd2a8124c94-file_1555694229984)

```
public String longestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0) return "";
        return longestCommonPrefix(strs, 0 , strs.length - 1);
}

private String longestCommonPrefix(String[] strs, int l, int r) {
    if (l == r) {
        //单个字符串
        return strs[l];
    } else {
        int mid = (l + r)/2;
        String lcpLeft =   longestCommonPrefix(strs, l , mid);
        String lcpRight =  longestCommonPrefix(strs, mid + 1,r);
        return commonPrefix(lcpLeft, lcpRight);
   }
}

String commonPrefix(String left,String right) {
    int min = Math.min(left.length(), right.length());
    for (int i = 0; i < min; i++) {
        if ( left.charAt(i) != right.charAt(i) )
            return left.substring(0, i);
    }
    return left.substring(0, min);
}
```

> **复杂度分析**
> 最坏情况下，我们有 n 个长度为 m 的相同字符串。
> - 时间复杂度：O(S), S 是所有字符串中字符数量的总和，S = m * n。
> 时间复杂度的递推式为 T(n)=2⋅T(n/2)+O(m)， 化简后可知其就是 O(S)。最好情况下，算法会进行 minLen ⋅ n 次比较，其中 minLen 是数组中最短字符串的长度。
> - 空间复杂度：O(m * log(n))
> 内存开支主要是递归过程中使用的栈空间所消耗的。 一共会进行 log(n) 次递归，每次需要 m 的空间存储返回结果，所以空间复杂度为 O(m⋅log(n))。

### 4.二分查找
**思路：** 每次丢弃一半查找区间
**算法：** 这个想法是应用二分查找法找到所有字符串的公共前缀的最大长度 L。 算法的查找区间是 (0…minLen)，其中 minLen 是输入数据中最短的字符串的长度，同时也是答案的最长可能长度。 每一次将查找区间一分为二，然后丢弃一定不包含最终答案的那一个。算法进行的过程中一共会出现两种可能情况：

- S[1...mid] **不是所有串的公共前缀**。 这表明对于所有的 j > i S[1..j] 也不是公共前缀，于是我们就可以丢弃后半个查找区间。

- S[1...mid] **是所有串的公共前缀**。 这表示对于所有的 i < j S[1..i] 都是可行的公共前缀，因为我们要找最长的公共前缀，所以我们可以把前半个查找区间丢弃。

![](https://pic.leetcode-cn.com/e41778494b56890e2bb7616504e2a0169bbdb409710262eaf5250c635adab9d6-file_1555694009677)

```
public String longestCommonPrefix(String[] strs) {
    if (strs == null || strs.length == 0)
        return "";
    int minLen = Integer.MAX_VALUE;
    //得出最小长度
    for (String str : strs)
        minLen = Math.min(minLen, str.length());
    int low = 1;
    int high = minLen;
    while (low <= high) {
        int middle = (low + high) / 2;
        if (isCommonPrefix(strs, middle))
            low = middle + 1;
        else
            high = middle - 1;
    }
    return strs[0].substring(0, (low + high) / 2);
}

private boolean isCommonPrefix(String[] strs, int len){
    String str1 = strs[0].substring(0,len);
    for (int i = 1; i < strs.length; i++)
        if (!strs[i].startsWith(str1))
            return false;
    return true;
}
```
> **复杂度分析**
> 最坏情况下，我们有 n 个长度为 m 的相同字符串。
> - 时间复杂度：O(S * log(n)), 其中 S 是所有字符串中字符数量的总和，S = m * n。
> 算法一共会进行 log(n) 次迭代，每次一都会进行 S = m*n 次比较，所以总时间复杂度为 O(S⋅log(n))。
> - 空间复杂度：O(1)

### 5.字典树
[题解](https://leetcode-cn.com/problems/longest-common-prefix/solution/zui-chang-gong-gong-qian-zhui-by-leetcode/)
![](https://pic.leetcode-cn.com/093a52aeacfa1f4b5489bbee3a6d0de22c9dcde6dd72a1c1887f3b75f3eec749-file_1555694178934)

## 其他题解
### 1.
**思路：** 排除一些特殊情况，**从后向前**查找公共前缀

```
public String longestCommonPrefix(String[] strs) {
    if (strs.length == 0) {
        return "";
    }
    if (strs.length == 1) {
        return strs[0];
    }
    String min = strs[0] ;
    for (int i = 0; i < strs.length; i++) {
        if (strs[i].isEmpty()) {
            return "";
        }
        if (strs[0].charAt(0) != strs[i].charAt(0)) {
            return "";
        }
        if (strs[i].length() <= min.length()) {
            min = strs[i];
        }
    }
    //比较末端字符串字符
    for (int i = 0; i < strs.length; i++) {
        if (min.equals(strs[i])) {
            continue;
        }
        for (int j = min.length()-1; j > 0 ; j--) {
            if (min.charAt(j) != strs[i].charAt(j)) {
                min = min.substring(0, j);
            }
        }
    }
    return min;
}
```

### 2.python的一种解法
**思路：** 将字符串数组反向放入迭代器输出，等于是反向判断各字符串相同位置是否相同。
```
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        L = zip(*strs)
        # list(zip(*["abc","efg","jk"])) --例子输出-→ [('a', 'e', 'j'), ('b', 'f', 'k')] # 加*表示反向zip()

        r = [len(set(c)) == 1 for c in L] + [False]
        # set([1,1,0,1]) --例子输出-→ [1,0] # set()删除重复元素

        if strs != []:
            s = r.index(False)  # 查找第一个False的下标
            return strs[0][0:s]  # 列表查找+切片
        else:
            return ''
```
### 3.字符串数组排序
**思路：** 对字符串数组排序，比较第一个和最后一个公共前缀
```
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs == null || strs.length == 0) return "";
        StringBuilder res = new StringBuilder();
        Arrays.sort(strs);
        // 字符串转数组
        char[] a = strs[0].toCharArray();
        char[] b = strs[strs.length - 1].toCharArray();
        for (int i = 0; i < a.length; i++) {
            if (i < b.length && a[i] == b[i]) {
                res.append(a[i]);
            }
            else{
                break;
            }
        }
        return res.toString();

    }
}
```

---
***参考：
[领扣](https://leetcode-cn.com/problems/two-sum/solution/liang-shu-zhi-he-by-leetcode-2/)
[python](https://leetcode-cn.com/problems/longest-common-prefix/solution/2-xing-python-by-knifezhu-2/)
[powcai](https://leetcode-cn.com/problems/longest-common-prefix/solution/duo-chong-si-lu-qiu-jie-by-powcai-2/)***
