# Longest Palindromic Substring

## 原题

[Longest Palindromic Substring](https://leetcode.com/explore/interview/card/top-interview-questions-medium/103/array-and-strings/780/)

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"
Output: "bb"
```

## 解题

题目的意思就是找出字符串中最长的回文子串

### 方法1

最直接的方法，通过双重遍历来判断回文子串。主要是要注意子串为奇数偶数的情况。

```java
public String longestPalindrome(String s) {
    if (s.equals("") || s.length() == 1) {
        return s;
    }
    String str = s.substring(0, 1);
    for (int i = 0; i < s.length() - 1; i++) {
        String s1 = isPalindrome(s, i, i);
        String s2 = isPalindrome(s, i, i + 1);
        String s3 = s1.length() > s2.length() ? s1 : s2;
        str = s3.length() > str.length() ? s3 : str;
    }

    return str;
}

private String isPalindrome(String s, int left, int right) {
    while (left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)) {
        left--;
        right++;
    }
    return s.substring(left + 1, right);
}
```

