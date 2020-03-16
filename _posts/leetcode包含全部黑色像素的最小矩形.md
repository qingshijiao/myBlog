---
title: 302.包含全部黑色像素的最小矩形(Smallest Rectangle Enclosing Black Pixels)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
题目：

An image is represented by a binary matrix with 0 as a white pixel and 1 as a black pixel. The black pixels are connected, i.e., there is only one black region. Pixels are connected horizontally and vertically. Given the location (x, y) of one of the black pixels, return the area of the smallest (axis-aligned) rectangle that encloses all black pixels.

For example, given the following image:
```
[
  "0010",
  "0110",
  "0100"
]
and x = 0, y = 2,

Return 6.
```

#### Solution

Language: **Java**

```java
​public class Solution {
    public int minArea(char[][] image, int x, int y) {
        if(image == null || image.length == 0 || image[0].length == 0){
            return 0;
        }
        int m = image.length;
        int n = image[0].length;

        if(x<0 || x>=m || y<0 || y>=n){
            return 0;
        }

        int left = binarySearch(image, 0, y, 0, m, true, true); //左边第一个 '1'
        int right = binarySearch(image, y+1, n, 0, m, true, false); //右边第一个 '0'
        int up = binarySearch(image, 0, x, 0, n, false, true); // 上边第一个 '1'
        int down = binarySearch(image, x+1, m, 0, n, false, false); //下边第一个 '0'

        return (right-left) * (down - up);
    }

    private int binarySearch(char [][] image, int low, int high, int min, int max, boolean searchHor, boolean searchFirstOne){
        while(low < high){
            int mid = low + (high - low)/2;

            boolean existBlack = false;
            for(int i = min; i<max; i++){
                if((searchHor ? image[i][mid] : image[mid][i]) == '1'){
                    existBlack = true;
                    break;
                }
            }

            if(existBlack == searchFirstOne){
                high = mid;
            }else{
                low = mid+1;
            }
        }
        return low;
    }
}
```

---
***参考：
[Dylan_Java_NYC](https://www.cnblogs.com/Dylan-Java-NYC/p/5318027.html)***
