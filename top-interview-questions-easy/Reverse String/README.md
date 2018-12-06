# Reverse String

## 原题

[Reverse String](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/879/)

Write a function that takes a string as input and returns the string reversed.

**Example:**
Given s = "hello", return "olleh".

## 解题

题目意思就是翻转这个字符串。最直接的就是从后往前遍历然后赋值到新的字符串中，这种方法就不写了。

### 方法1

交换首位的字符串，比直接倒叙赋值少n/2时间

```java
	// O(n/2)
    public String reverseString(String s) {
        char[] cs = s.toCharArray();
        int n = cs.length;
        for (int i = 0; i < n / 2; i++) {
            char temp = cs[i];
            cs[i] = cs[n - 1 - i];
            cs[n - 1 - i] = temp;
        }
        return new String(cs);
    }
```

### 方法2

和方法1原理一样，只不过交换的时候用异或方法，减少一个temp的中间变量。

异或交换原理:[[异或的性质及运用](http://www.cnblogs.com/suoloveyou/archive/2012/04/25/2470292.html)]

```java
	public String reverseString(String s) {
        char[] cs = s.toCharArray();
        int n = cs.length;
        for (int i = 0; i < n / 2; i++) {
            cs[i] = (char) (cs[i] ^ cs[n - 1 - i]);
            cs[n - 1 - i] = (char) (cs[n - 1 - i] ^ cs[i]);
            cs[i] = (char) (cs[i] ^ cs[n - 1 - i]);

        }
        return new String(cs);
    }
```

### 方法3

用栈的先进后出原理

```java
	public String reverseString(String s) {
        Stack<Character> stack = new Stack<>();
        char[] cs = s.toCharArray();

        for (char c : cs) {
            stack.push(c);
        }
        int len = cs.length;
        for (int i = 0; i < len; i++) {
            cs[i] = stack.pop();
        }
        return new String(cs);
    }
```

### 方法4

用递归，每个循环中都将字符串翻转

```java
	public String reverseString(String s) {
        if (s.length() <= 1) {
            return s;
        }
        String left = s.substring(0, s.length() / 2);
        String right = s.substring(s.length() / 2, s.length());
        return reverseString(right) + reverseString(left);
    }
```

