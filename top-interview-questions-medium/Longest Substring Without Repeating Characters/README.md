# Longest Substring Without Repeating Characters

## 原题

[Longest Substring Without Repeating Characters](https://leetcode.com/explore/interview/card/top-interview-questions-medium/103/array-and-strings/779/)

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

**Example 2:**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```

## 解题

题目的意思就是获取一个字符串中，不含重复字母的最大子串的长度。

### 方法1

遍历字符串，利用HashSet的不重复性来判断字符串里下一个字符是否在子串里存在，如果不存在，继续往下遍历，否则就跳回到子串开始的地方的下一个位置再次开始新的子串计算。

```java
public int lengthOfLongestSubstring(String s) {
    char[] cs = s.toCharArray();
    Set<Character> set = new HashSet<>();
    int positon = 0, length = 0, maxLength = 0;
    for (int i = 0; i < cs.length; i++) {
        if (set.add(cs[i])) {
            length++;
        } else {
            if (length > maxLength) {
                maxLength = length;
            }
            length = 0;
            set.clear();
            i = positon++;
        }
    }

    return length > maxLength ? length : maxLength;
}
```

