---
title: 20.有效的括号（Valid Parentheses）

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
# 题目
给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。

有效字符串需满足：

1. 左括号必须用相同类型的右括号闭合。
2. 左括号必须以正确的顺序闭合。

注意空字符串可被认为是有效字符串。

示例 1:
> 输入: "()"
> 输出: true

示例 2:
> 输入: "()[]{}"
> 输出: true

示例 3:
> 输入: "(]"
> 输出: false

示例 4:
> 输入: "([)]"
> 输出: false

示例 5:
> 输入: "{[]}"
> 输出: true


# 题解

## 官方题解
### 1.栈
**思路：** 排除内层有效括号，使用栈。栈中i只存储了左括号，右括号用于推出栈顶元素并与之配对。
![](https://pic.leetcode-cn.com/Figures/20/STACK-3.png)

```
class Solution {

  // Hash table that takes care of the mappings.
  private HashMap<Character, Character> mappings;

  // Initialize hash map with mappings. This simply makes the code easier to read.
  public Solution() {
    this.mappings = new HashMap<Character, Character>();
    this.mappings.put(')', '(');
    this.mappings.put('}', '{');
    this.mappings.put(']', '[');
  }

  public boolean isValid(String s) {

    // Initialize a stack to be used in the algorithm.
    Stack<Character> stack = new Stack<Character>();

    for (int i = 0; i < s.length(); i++) {
      char c = s.charAt(i);

      // If the current character is a closing bracket.
      if (this.mappings.containsKey(c)) {

        // Get the top element of the stack. If the stack is empty, set a dummy value of '#'
        char topElement = stack.empty() ? '#' : stack.pop();

        // If the mapping for this bracket doesn't match the stack's top element, return false.
        if (topElement != this.mappings.get(c)) {
          return false;
        }
      } else {
        // If it was an opening bracket, push to the stack.
        stack.push(c);
      }
    }

    // If the stack still contains elements, then it is an invalid expression.
    return stack.isEmpty();
  }
}
```
**复杂度分析：**
- 时间复杂度：O(n)，因为我们一次只遍历给定的字符串中的一个字符并在栈上进行 O(1) 的推入和弹出操作。
- 空间复杂度：O(n)，当我们将所有的开括号都推到栈上时以及在最糟糕的情况下，我们最终要把所有括号推到栈上。例如 ((((((((((。

## 其他题解
### 1.条件判断
**思路：** 不使用 map 存储，直接使用条件判断。
```
class Solution {
    public boolean isValid(String s) {
      boolean result = true;
      Stack<Character> stack = new Stack<Character>();
      // 遇到左括号压栈，遇到右括号弹出栈顶元素并匹配
      // 若匹配失败，或者栈已空，则表达式无效
      // 匹配结束，若栈非空，表达式无效
      for (int i = 0; i < s.length() && result; i++) {
        char a = s.charAt(i);
        if (a == '(' || a == '[' || a== '{') {
          stack.add(a);
          } else if (a == ')') {
            result = !stack.isEmpty() && '(' == stack.pop();
          } else if (a == ']') {
            result = !stack.isEmpty() && '[' == stack.pop();
          } else if (a == '}') {
            result = !stack.isEmpty() && '{' == stack.pop();
          }
      }
      return result && stack.isEmpty();
    }
}
```

### 2.括号消消乐(时间过长)
**思路：** 每找到一个有效括号，消去。
```
class Solution {
        public boolean isValid(String s) {

        while (s.contains("{}")||s.contains("[]")|| s.contains("()")){

            if(s.contains("{}")) s=s.replace("{}","");
            if(s.contains("()")) s=s.replace("()","");
            if(s.contains("[]")) s=s.replace("[]","");

        }

        return s.isEmpty();
    }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/valid-parentheses)
[mrhkang](https://leetcode-cn.com/problems/two-sum/solution/java-zhan-by-mrhkang/)
[td0Gn7z2GP](https://leetcode-cn.com/problems/two-sum/solution/you-xiao-de-gua-hao-java-by-td0gn7z2gp/)***
