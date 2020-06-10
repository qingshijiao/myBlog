---
title: 468. 验证IP地址 (Validate IP Address)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [468\. 验证IP地址](https://leetcode-cn.com/problems/validate-ip-address/)

Difficulty: **中等**


编写一个函数来验证输入的字符串是否是有效的 IPv4 或 IPv6 地址。

**IPv4** 地址由十进制数和点来表示，每个地址包含4个十进制数，其范围为 0 - 255， 用(".")分割。比如，`172.16.254.1`；

同时，IPv4 地址内的数不会以 0 开头。比如，地址 `172.16.254.01` 是不合法的。

**IPv6** 地址由8组16进制的数字来表示，每组表示 16 比特。这些组数字通过 (":")分割。比如,  `2001:0db8:85a3:0000:0000:8a2e:0370:7334` 是一个有效的地址。而且，我们可以加入一些以 0 开头的数字，字母可以使用大写，也可以是小写。所以， `2001:db8:85a3:0:0:8A2E:0370:7334` 也是一个有效的 IPv6 address地址 (即，忽略 0 开头，忽略大小写)。

然而，我们不能因为某个组的值为 0，而使用一个空的组，以至于出现 (::) 的情况。 比如， `2001:0db8:85a3::8A2E:0370:7334` 是无效的 IPv6 地址。

同时，在 IPv6 地址中，多余的 0 也是不被允许的。比如， `02001:0db8:85a3:0000:0000:8a2e:0370:7334` 是无效的。

**说明:** 你可以认为给定的字符串里没有空格或者其他特殊字符。

**示例 1:**

```
输入: "172.16.254.1"

输出: "IPv4"

解释: 这是一个有效的 IPv4 地址, 所以返回 "IPv4"。
```

**示例 2:**

```
输入: "2001:0db8:85a3:0:0:8A2E:0370:7334"

输出: "IPv6"

解释: 这是一个有效的 IPv6 地址, 所以返回 "IPv6"。
```

**示例 3:**

```
输入: "256.256.256.256"

输出: "Neither"

解释: 这个地址既不是 IPv4 也不是 IPv6 地址。
```


#### Solution

Language: **Java**

```java
​class Solution {
    public String validIPAddress(String IP) {
        int check = check(IP);
        if(check == 1 && checkIpv4(IP)) return "IPv4";
        if(check == 2 && checkIPv6(IP)) return "IPv6";
        return "Neither";
    }

    private static int check(String ip){

        // 判断是否是 IPv6
        if(ip.lastIndexOf(':') != -1) {
            // 不能有点
            if(ip.lastIndexOf('.') != -1) return 0;
            if(ip.length() < 15 || ip.length() > 39) return 0;
            if(ip.lastIndexOf(':') == ip.length() - 1) return 0;
            if(ip.indexOf(':') == 0) return 0;
            return 2;
        }
        if(ip.lastIndexOf('.') != -1){

            if(ip.lastIndexOf(':') != -1) return 0;
            if(ip.length() < 7 || ip.length() > 15) return 0;
            if(ip.lastIndexOf('.') == ip.length() - 1) return 0;
            if(ip.indexOf('.') == 0) return 0;
            return 1;
        }
        return 0;
    }

    private static boolean checkIPv6(String ip) {

        // 格式符合的 IPv6
        char[] chars = ip.toCharArray();
        int low = 0;
        int points = 0;
        for (int i = 0; i < chars.length; i++) {
            if(!isVaildLetter(chars[i])) return false;
            if(chars[i] != ':') continue;
            ++points;
            if(!isVaild_ip6(chars,low,i - 1)) return false;
            low = i + 1;
        }
        return points == 7 && isVaild_ip6(chars,low,chars.length - 1);
    }

    private static boolean checkIpv4(String ip) {

        // 格式符合条件的 IPv4
        char[] chars = ip.toCharArray();
        int low = 0;
        int points = 0;
        for (int i = 0; i < chars.length; i++) {
            if(!isNumber(chars[i])) return false;
            if(chars[i] != '.') continue;
            ++points;
            if(!isVaild_ip4(chars,low,i - 1)) return false;
            low = i + 1;
        }
        return points == 3 && isVaild_ip4(chars,low,chars.length - 1);

    }

    private static boolean isVaild_ip4(char[] cs,int low, int high){

        if(high - low > 2) return false;
        if(cs[low] == '.') return false;
        if(high == low) return true;
        if(cs[low] == '0') return false;
        if(high == low + 1) return true;
        // 3
        if(cs[low] == '1') return true;
        if(cs[low] > '2') return false;
        if(cs[low + 1] > '5') return false;
        if(cs[low + 1] < '5') return true;
        if(cs[high] > '5') return false;
        return true;
    }

    private static boolean isNumber(char c) {
        return c >= '0' && c <= '9' || c == '.';
    }

    private static boolean isVaild_ip6(char[] chars, int low, int high) {

        if(high - low > 3) return false;
        if(chars[low] == ':') return false;
        return true;
    }

    private static boolean isVaildLetter(char c){

        return (c >= '0' && c <= '9') || (c >= 'a' && c <= 'f') || (c >= 'A' && c <= 'F') || c == ':';
    }
    
}
```

---
***参考:
[leetcode](https://leetcode-cn.com/problems/validate-ip-address/)***
