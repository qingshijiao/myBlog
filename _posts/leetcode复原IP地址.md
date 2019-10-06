---
title: 93.复原IP地址（Restore IP Addresses）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个只包含数字的字符串，复原它并返回所有可能的 IP 地址格式。

示例:
```
输入: "25525511135"
输出: ["255.255.11.135", "255.255.111.35"]
```

# 题解

## 官方题解
### 1.回溯算法
**思路：**
IP地址是由32位二进制数组成，人们为了方便记忆，就将组成计算机的IP地址的32位二进制分成四段，每段8位，中间用小数点隔开，然后将每八位二进制转换成十进制数。

![](https://pic.leetcode-cn.com/179d7d352cda8c2703f068326cfc4e4d8591cef719245ef18ac676f7d2cafb8e-image.png)

```
class Solution {
  int n;
  String s;
  LinkedList<String> segments = new LinkedList<String>();
  ArrayList<String> output = new ArrayList<String>();

  public boolean valid(String segment) {
    /*
    Check if the current segment is valid :
    1. less or equal to 255
    2. the first character could be '0'
    only if the segment is equal to '0'
    */
    int m = segment.length();
    if (m > 3)
      return false;
    return (segment.charAt(0) != '0') ? (Integer.valueOf(segment) <= 255) : (m == 1);
  }

  public void update_output(int curr_pos) {
    /*
    Append the current list of segments
    to the list of solutions
    */
    String segment = s.substring(curr_pos + 1, n);
    if (valid(segment)) {
      segments.add(segment);
      output.add(String.join(".", segments));
      segments.removeLast();
    }
  }

  public void backtrack(int prev_pos, int dots) {
    /*
    prev_pos : the position of the previously placed dot
    dots : number of dots to place
    */
    // The current dot curr_pos could be placed
    // in a range from prev_pos + 1 to prev_pos + 4.
    // The dot couldn't be placed
    // after the last character in the string.
    int max_pos = Math.min(n - 1, prev_pos + 4);
    for (int curr_pos = prev_pos + 1; curr_pos < max_pos; curr_pos++) {
      String segment = s.substring(prev_pos + 1, curr_pos + 1);
      if (valid(segment)) {
        segments.add(segment);  // place dot
        if (dots - 1 == 0)      // if all 3 dots are placed
          update_output(curr_pos);  // add the solution to output
        else
          backtrack(curr_pos, dots - 1);  // continue to place dots
        segments.removeLast();  // remove the last placed dot
      }
    }
  }

  public List<String> restoreIpAddresses(String s) {
    n = s.length();
    this.s = s;
    backtrack(-1, 3);
    return output;
  }
}

```
**复杂度分析：**
- 时间复杂度： 如上文所述，需要检查的组合不多于27个。
- 空间复杂度：常数空间存储解，不多于19 个有效IP地址。
![](https://pic.leetcode-cn.com/3baa385fecae6239495c19c88a279f4b76752a7a089fabdf15685e829b8e0a73-image.png)


## 其他题解
### 1.暴力法
**思路：**

```
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        int n = s.length();
        for (int i = 0; i < 3; i++) {
            for (int j = i + 1; j < i + 4; j++) {
                for (int k = j + 1; k < j + 4; k++) {
                    if (i < n && j < n && k < n) {
                        String tmp1 = s.substring(0, i + 1);
                        String tmp2 = s.substring(i + 1, j + 1);
                        String tmp3 = s.substring(j + 1, k + 1);
                        String tmp4 = s.substring(k + 1);
                        if (helper(tmp1) && helper(tmp2) && helper(tmp3) && helper(tmp4))
                            res.add(tmp1 + "." + tmp2 + "." + tmp3 + "." + tmp4);
                    }
                }
            }
        }
        return res;
    }

    private boolean helper(String tmp) {
        if (tmp == null || tmp.length() == 0 || tmp.length() > 3 || (tmp.charAt(0) == '0' && tmp.length() > 1) || Integer.parseInt(tmp) > 255)
            return false;
        return true;
    }
}

```

### 2.回溯法
**思路：**

```
class Solution {
    public List<String> restoreIpAddresses(String s) {
        List<String> res = new ArrayList<>();
        int n = s.length();
        backtrack(0, "", 4, s, res, n);
        return res;
    }

    private void backtrack(int i, String tmp, int flag, String s, List<String> res, int n) {
        if (i == n && flag == 0) {
            res.add(tmp.substring(0, tmp.length() - 1));
            return;
        }
        if (flag < 0) return;
        for (int j = i; j < i + 3; j++) {
            if (j < n) {
                if (i == j && s.charAt(j) == '0') {
                    backtrack(j + 1, tmp + s.charAt(j) + ".", flag - 1, s, res, n);
                    break;
                }
                if (Integer.parseInt(s.substring(i, j + 1)) <= 255)
                    backtrack(j + 1, tmp + s.substring(i, j + 1) + ".", flag - 1, s, res, n);
            }
        }
    }
}
```



---
***参考：
[LeetCode](https://leetcode-cn.com/problems/restore-ip-addresses/solution/fu-yuan-ipdi-zhi-by-leetcode/)
[powcai](https://leetcode-cn.com/problems/restore-ip-addresses/solution/bao-li-he-hui-su-by-powcai/)***
