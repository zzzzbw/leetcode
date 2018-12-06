# Valid Parentheses 

## 原题

[Valid Parentheses ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/721/)

Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

**Example 1:**

```
Input: "()"
Output: true
```

**Example 2:**

```
Input: "()[]{}"
Output: true
```

**Example 3:**

```
Input: "(]"
Output: false
```

**Example 4:**

```
Input: "([)]"
Output: false
```

**Example 5:**

```
Input: "{[]}"
Output: true
```

## 解题

这题的意思就是判断一个数组里面的括号是否配对

### 方法1

看到这种题，简直就是最经典的栈的应用场景，先入后出的特性。唯一要注意的就是防止栈空的时候pop和判断最后要看栈是否为空。

```java
public boolean isValid(String s) {
    char[] cs = s.toCharArray();
    Stack<Character> stack = new Stack<>();
    for (char c : cs) {
        if (c == '{' || c == '(' || c == '[') {
            stack.push(c);
        } else if (stack.isEmpty()) {
            return false;
        } else if (c == '}') {
            if (!stack.pop().equals('{')) {
                return false;
            }
        } else if (c == ')') {
            if (!stack.pop().equals('(')) {
                return false;
            }
        } else if (c == ']') {
            if (!stack.pop().equals('[')) {
                return false;
            }
        }
    }
    if(!stack.isEmpty()) {
        return false;
    }
    return true;
}
```

