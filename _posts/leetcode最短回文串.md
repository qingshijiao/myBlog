---
title: 214.最短回文串（Shortest Palindrome）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [214\. 最短回文串](https://leetcode-cn.com/problems/shortest-palindrome/)

Difficulty: **困难**


给定一个字符串 _**s**_，你可以通过在字符串前面添加字符将其转换为回文串。找到并返回可以用这种方式转换的最短回文串。

**示例 1:**

```
输入: "aacecaaa"
输出: "aaacecaaa"
```

**示例 2:**

```
输入: "abcd"
输出: "dcbabcd"
```


#### Solution1 反转 + 递归

Language: **Java**

```java
​public class Solution {
    public String shortestPalindrome(String s) {
        int i = 0, n = s.length();
        for (int j = n - 1; j >= 0; --j) {
            if (s.charAt(i) == s.charAt(j)) ++i;
        }
        if (i == n) return s;
        String rem = s.substring(i);
        String rem_rev = new StringBuilder(rem).reverse().toString();
        return rem_rev + shortestPalindrome(s.substring(0, i)) + rem;
    }
}
```

#### Solution2 KMP

Language: **Java**

```java
​public class Solution {
    public string ShortestPalindrome(string s)
        {
            if (s.Length == 0 || s.Length == 1) return s;
            var new_string = s + '#' + new string(s.Reverse().ToArray()); // 把字符串和字符串的逆序连接起来 如果有正序字符串的前缀和逆序字符串的后缀相同 说明这部分已经是回文序列了
            var next = GetNext(new_string);
            return new string(s.Substring(next.Last()).Reverse().ToArray()) + s; // 把不是回文序列的部分的逆序添上
        }
        public List<int> GetNext(string s) // 求next数组
        {
            var next = new List<int>(s.Length + 1);
            next.Add(-1);
            var j = 0;
            var k = -1;
            while (j != s.Length)
            {
                if (k == -1 || s[j] == s[k])
                {
                    ++j;
                    next.Add(++k);
                }
                else
                {
                    k = next[k];
                }
            }
            return next;
        }
}
```


#### Solution3 马拉车算法

Language: **Java**

```java
class Solution {
    public String shortestPalindrome(String s) {
        char[] chars = manacherReverseString(s);//反转之后的
        int[] parr = new int[chars.length];
        int R = -1;
        int C = -1;
        int L = -1;
        for(int i=0; i<parr.length; i++){
            parr[i] = i>R ? 1 : Math.min(parr[2*C-i], R-i);
            while(i+parr[i]<parr.length && i-parr[i]>-1){
                if(chars[i+parr[i]] == chars[i-parr[i]]){
                    parr[i]++;
                }
                else{
                    break;
                }
            }
            if(R<i+parr[i]){
                R = i+parr[i]-1;
                C = i;
            }
            if(R==parr.length-1){
                L = 2*C-R;
                break;
            }
        }
        StringBuilder ret = new StringBuilder();
        ret.append(chars, 0, L);
        for(int i=chars.length-1; i>=0; i--){
            ret.append(chars[i]);
        }
        return ret.toString().replace("#", "");
    }

    private char[] manacherReverseString(String s){
        char[] source = s.toCharArray();
        char[] ret = new char[s.length()*2+1];
        for(int i=0; i<ret.length; i++){
            ret[i] = i%2==0 ? '#' : source[source.length-i/2-1];
        }
        return ret;
    }
}

```

#### Solution4 中心扩展法

Language: **Java**

```java
class Solution {
    private String result = "";

    public boolean through(String s, int l, int r) {
        while (l >= 0) {
            if (r >= s.length()) return false;
            if (s.charAt(l) != s.charAt(r)) return false;
            l--;
            r++;
        }
        return true;
    }

    public String shortestPalindrome(String s) {
        if (null == s) return null;
        if (s.length() <= 1) return s;
        for (int i = 0; i <= s.length() / 2; i++) {
            if (through(s, i, i) && ((i + 1) * 2 - 1) <= s.length()) {
                String sub = s.substring(0, (i + 1) * 2 - 1);
                result = result.length() < sub.length() ? sub : result;
            }
            if (through(s, i, i + 1) && ((i + 1) * 2) <= s.length()) {
                String sub = s.substring(0, (i + 1) * 2);
                result = result.length() < sub.length() ? sub : result;
            }
        }
        if (result.length() == s.length()) return result;
        String sub = s.substring(result.length(), s.length());
        String reverseSub = new StringBuilder(sub).reverse().toString();
        return reverseSub + result + sub;
    }
}

```


---
***参考：
[LeetCode](https://leetcode-cn.com/problems/shortest-palindrome/solution/zui-duan-hui-wen-chuan-by-leetcode/)
[exonuclease](https://leetcode-cn.com/problems/shortest-palindrome/solution/li-yong-kmpli-mian-de-nextshu-zu-by-exonuclease/)
[Enpong](https://leetcode-cn.com/problems/shortest-palindrome/solution/ma-la-che-by-enpong/)
[grw](https://leetcode-cn.com/problems/shortest-palindrome/solution/zhong-xin-kuo-san-fa-java-by-grw/)***
