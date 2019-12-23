---
title: 249.移位字符串分组（Displacement tandem grouping）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---

给定一个字符串，对该字符串可以进行 “移位” 的操作，也就是将字符串中每个字母都变为其在字母表中后续的字母，比如："abc" -> "bcd"。这样，我们可以持续进行 “移位” 操作，从而生成如下移位序列：

"abc" -> "bcd" -> ... -> "xyz"
给定一个包含仅小写字母字符串的列表，将该列表中所有满足 “移位” 操作规律的组合进行分组并返回。

示例：
```
输入: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"]
输出: 
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
```

#### Solution

Language: **Java**

```java

class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        List<List<String>> result = new ArrayList<List<String>>();
        HashMap<String, ArrayList<String>> map
                        = new HashMap<String, ArrayList<String>>();

        for(String s: strings){
            char[] arr = s.toCharArray();
            if(arr.length>0){
                int diff = arr[0]-'a';
                for(int i=0; i<arr.length; i++){
                    if(arr[i]-diff<'a'){
                       arr[i] = (char) (arr[i]-diff+26);
                    }else{
                       arr[i] = (char) (arr[i]-diff);
                    }

                }
            }

            String ns = new String(arr);
            if(map.containsKey(ns)){
                map.get(ns).add(s);
            }else{
                ArrayList<String> al = new ArrayList<String>();
                al.add(s);
                map.put(ns, al);
            }
        }

        for(Map.Entry<String, ArrayList<String>> entry: map.entrySet()){
            Collections.sort(entry.getValue());
        }

        result.addAll(map.values());

        return result;
    }
}

```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/group-shifted-strings/)
[轻风舞动](https://www.cnblogs.com/lightwindy/p/8727587.html)***
