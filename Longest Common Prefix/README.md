# Longest Common Prefix

## 原题

[Longest Common Prefix](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/887/)

Write a function to find the longest common prefix string amongst an array of strings.

## 解题

题目意思就是找出一组字符串中最长的公共前缀

### 方法1

循环遍历数组，和strs[0]的字符从头比对，知道有不相同的为止，然后把相同的前缀放到strs[0]中。

```java
   public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        int i = 1, j = 0;
        while (i < strs.length && !strs[0].isEmpty()) {
            StringBuilder sBuilder = new StringBuilder();
            j = 0;
            while (j < strs[0].length() && j < strs[i].length()) {
                if (strs[i].charAt(j) == strs[0].charAt(j)) {
                    sBuilder.append(strs[0].charAt(j));
                } else {
                    strs[0] = sBuilder.toString();
                    break;
                }
                j++;
            }
            strs[0] = sBuilder.toString();
            i++;
        }

        return strs[0];
    }
```

### 方法2

和方法1类似，只不过方法1是从头开始比对，这个方法是每次都截length() - 1的长度来比对是否是前缀。

```java
	public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        for (String str : strs) {
            while (str.indexOf(strs[0]) != 0) {
                strs[0] = strs[0].substring(0, strs[0].length() - 1);
            }
            if (strs[0].isEmpty()) {
                return strs[0];
            }
        }
        return strs[0];
    }
```

### 方法3

获取两个字符串的公共前缀，然后不停的递归整个数组两两字符串的公共前缀，最后就是得出的数组的公共前缀。

```java
   public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) {
            return "";
        }
        return commonPrefix(strs, 0, strs.length - 1);
    }

    private String commonPrefix(String[] strs, int start, int end) {
        if (start >= end) {
            return strs[start];
        }

        int mid = (start + end) / 2;
        String left = commonPrefix(strs, start, mid);
        String right = commonPrefix(strs, mid + 1, end);

        int min = Math.min(left.length(), right.length());
        for (int i = 0; i < min; i++) {
            if (left.charAt(i) != right.charAt(i))
                return left.substring(0, i);
        }
        return left.substring(0, min);
    }
```

