---
title: 301.删除无效的括号(Remove Invalid Parentheses)

date: {{date}}
categories:
- leetcode
tags:
- leetcode

---
### [301\. 删除无效的括号](https://leetcode-cn.com/problems/remove-invalid-parentheses/)

Difficulty: **困难**


删除最小数量的无效括号，使得输入的字符串有效，返回所有可能的结果。

**说明:** 输入可能包含了除 `(` 和 `)` 以外的字符。

**示例 1:**

```
输入: "()())()"
输出: ["()()()", "(())()"]
```

**示例 2:**

```
输入: "(a)())()"
输出: ["(a)()()", "(a())()"]
```

**示例 3:**

```
输入: ")("
输出: [""]
```


#### Solution1 - 回溯

Language: **Java**

```java
​class Solution {

  private Set<String> validExpressions = new HashSet<String>();
  private int minimumRemoved;

  private void reset() {
    this.validExpressions.clear();
    this.minimumRemoved = Integer.MAX_VALUE;
  }

  private void recurse(
      String s,
      int index,
      int leftCount,
      int rightCount,
      StringBuilder expression,
      int removedCount) {

    // If we have reached the end of string.
    if (index == s.length()) {

      // If the current expression is valid.
      if (leftCount == rightCount) {

        // If the current count of removed parentheses is <= the current minimum count
        if (removedCount <= this.minimumRemoved) {

          // Convert StringBuilder to a String. This is an expensive operation.
          // So we only perform this when needed.
          String possibleAnswer = expression.toString();

          // If the current count beats the overall minimum we have till now
          if (removedCount < this.minimumRemoved) {
            this.validExpressions.clear();
            this.minimumRemoved = removedCount;
          }
          this.validExpressions.add(possibleAnswer);
        }
      }
    } else {

      char currentCharacter = s.charAt(index);
      int length = expression.length();

      // If the current character is neither an opening bracket nor a closing one,
      // simply recurse further by adding it to the expression StringBuilder
      if (currentCharacter != '(' && currentCharacter != ')') {
        expression.append(currentCharacter);
        this.recurse(s, index + 1, leftCount, rightCount, expression, removedCount);
        expression.deleteCharAt(length);
      } else {

        // Recursion where we delete the current character and move forward
        this.recurse(s, index + 1, leftCount, rightCount, expression, removedCount + 1);
        expression.append(currentCharacter);

        // If it's an opening parenthesis, consider it and recurse
        if (currentCharacter == '(') {
          this.recurse(s, index + 1, leftCount + 1, rightCount, expression, removedCount);
        } else if (rightCount < leftCount) {
          // For a closing parenthesis, only recurse if right < left
          this.recurse(s, index + 1, leftCount, rightCount + 1, expression, removedCount);
        }

        // Undoing the append operation for other recursions.
        expression.deleteCharAt(length);
      }
    }
  }

  public List<String> removeInvalidParentheses(String s) {

    this.reset();
    this.recurse(s, 0, 0, 0, new StringBuilder(), 0);
    return new ArrayList(this.validExpressions);
  }
}
```

```java
class Solution {
    public List<String> removeInvalidParentheses(String s) {
        int left = 0, right = 0;
        char[] cs = s.toCharArray();
        for(char c : cs) {
            if(c == '(') {
                left++;
            }else if(c == ')') {
                if(left == 0) right++;
                else left--;
            }
        }
        List<String> res = new ArrayList<>();
        backtrace(cs, 0, new StringBuilder(s.length()-left-right), res, 0, 0, left, right);
        return res;
    }

    private void backtrace(char[] cs, int cur, StringBuilder sb, List<String> res,
                           int left, int right, int remL, int remR) {
        if(cur == cs.length) {
            if(remL == 0 && remR == 0) res.add(sb.toString());
            return;
        }
        if(right > left) return;
        final int len = sb.length();
        if(cs[cur] == '(') {
            // use
            sb.append('(');
            backtrace(cs, cur+1, sb, res, left+1, right, remL, remR);
            sb.setLength(len);
            if(remL > 0) { // not use
                while(cur < cs.length && cs[cur] == '(') { // find next
                    cur++;
                    remL--;
                }
                if(remL >= 0) backtrace(cs, cur, sb, res, left, right, remL, remR);
            }
        }else if(cs[cur] == ')') {
            // use
            sb.append(')');
            backtrace(cs, cur+1, sb, res, left, right+1, remL, remR);
            sb.setLength(len);
            if(remR > 0) { // not use
                while(cur < cs.length && cs[cur] == ')') { // find next
                    cur++;
                    remR--;
                }
                if(remR >= 0) backtrace(cs, cur, sb, res, left, right, remL, remR);
            }
        }else {
            sb.append(cs[cur]);
            backtrace(cs, cur+1, sb, res, left, right, remL, remR);
            sb.setLength(len);
        }
    }

}
```

#### Solution2 - 有限的回溯

Language: **Java**

```java
​class Solution {

  private Set<String> validExpressions = new HashSet<String>();

  private void recurse(
      String s,
      int index,
      int leftCount,
      int rightCount,
      int leftRem,
      int rightRem,
      StringBuilder expression) {

    // If we reached the end of the string, just check if the resulting expression is
    // valid or not and also if we have removed the total number of left and right
    // parentheses that we should have removed.
    if (index == s.length()) {
      if (leftRem == 0 && rightRem == 0) {
        this.validExpressions.add(expression.toString());
      }

    } else {
      char character = s.charAt(index);
      int length = expression.length();

      // The discard case. Note that here we have our pruning condition.
      // We don't recurse if the remaining count for that parenthesis is == 0.
      if ((character == '(' && leftRem > 0) || (character == ')' && rightRem > 0)) {
        this.recurse(
            s,
            index + 1,
            leftCount,
            rightCount,
            leftRem - (character == '(' ? 1 : 0),
            rightRem - (character == ')' ? 1 : 0),
            expression);
      }

      expression.append(character);

      // Simply recurse one step further if the current character is not a parenthesis.
      if (character != '(' && character != ')') {

        this.recurse(s, index + 1, leftCount, rightCount, leftRem, rightRem, expression);

      } else if (character == '(') {

        // Consider an opening bracket.
        this.recurse(s, index + 1, leftCount + 1, rightCount, leftRem, rightRem, expression);

      } else if (rightCount < leftCount) {

        // Consider a closing bracket.
        this.recurse(s, index + 1, leftCount, rightCount + 1, leftRem, rightRem, expression);
      }

      // Delete for backtracking.
      expression.deleteCharAt(length);
    }
  }

  public List<String> removeInvalidParentheses(String s) {

    int left = 0, right = 0;

    // First, we find out the number of misplaced left and right parentheses.
    for (int i = 0; i < s.length(); i++) {

      // Simply record the left one.
      if (s.charAt(i) == '(') {
        left++;
      } else if (s.charAt(i) == ')') {
        // If we don't have a matching left, then this is a misplaced right, record it.
        right = left == 0 ? right + 1 : right;

        // Decrement count of left parentheses because we have found a right
        // which CAN be a matching one for a left.
        left = left > 0 ? left - 1 : left;
      }
    }

    this.recurse(s, 0, 0, 0, left, right, new StringBuilder());
    return new ArrayList<String>(this.validExpressions);
  }
}
```

---
***参考：
[LeetCode](https://leetcode-cn.com/problems/remove-invalid-parentheses/solution/shan-chu-wu-xiao-de-gua-hao-by-leetcode/)***
