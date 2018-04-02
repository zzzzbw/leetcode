# Implement strStr()

## 原题

[Implement strStr()](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/885/)

Implement [strStr()](http://www.cplusplus.com/reference/cstring/strstr/).

Return the index of the first occurrence of needle in haystack, or **-1** if needle is not part of haystack.

**Example 1:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```

**Example 2:**

```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```

## 解题

题目意思就是实现一个java的indexOf方法

### 方法1

就是循环遍历比对小字符串是否匹配大字符串的一部分，如果不匹配，则向前移动一位继续查找

```java
    //时间复杂度o(n^2)
	public int strStr(String haystack, String needle) {
        if (haystack.length() < needle.length()) {
            return -1;
        }
        char[] cs1 = haystack.toCharArray();
        char[] cs2 = needle.toCharArray();
        for (int i = 0; i < cs1.length - cs2.length + 1; i++) {
            boolean isIndex = true;
            for (int j = 0; j < cs2.length; j++) {
                if (cs1[i + j] != cs2[j]) {
                    isIndex = false;
                    break;
                }
            }
            if (isIndex) {
                return i;
            }
        }
        return -1;
    }
```

### 方法2-KMP算法

待续...