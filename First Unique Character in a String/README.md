# First Unique Character in a String

## 原题

[First Unique Character in a String](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/881/)

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Examples:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

**Note:** You may assume the string contain only lowercase letters.

## 解题

题目意思就是查找出这个字符串中第一个没有重复字母的字的位置，而且这个字符串里都是小写字母

### 方法1

这个方法就是双重遍历循环，然后把有重复的字符都变为' '空格，当遍历某个没有重复的，就是第一个不重复的

```java
   //时间复杂度O(n^2)
	public int firstUniqChar(String s) {
        char[] cs = s.toCharArray();
        if (cs.length == 1) {
            return 0;
        }

        for (int i = 0; i < cs.length; i++) {
            if (cs[i] == ' ') {
                continue;
            }
            boolean repeat = false;
            for (int j = i + 1; j < cs.length; j++) {
                if (cs[j] != ' ' && cs[j] == cs[i]) {
                    repeat = true;
                    cs[j] = ' ';
                }
            }
            if (!repeat) {
                return i;
            }
        }

        return -1;
    }
```

### 方法2

创建两个HashSet，一个用于保存所有出现过的char,当set.add返回false表示已存在时，把char存入repeat的set中。然后遍历repeat的set，remove掉重复出现的char，此时set中有的字符就是只出现一次的。最后再遍历这个set，找出在原先字符串的位置，返回最小的一个就是第一个不重复的字符。

```java
	//时间复杂度O(3n)
	public int firstUniqChar(String s) {
        char[] cs = s.toCharArray();
        Set<Character> set = new HashSet<>();
        Set<Character> repeat = new HashSet<>();
        for (char c : cs) {
            if (!set.add(c)) {
                repeat.add(c);
            }
        }
        for (char c : repeat) {
            if (set.contains(c)) {
                set.remove(c);
            }
        }

        int result = -1;
        for (char c : set) {
            int index = s.indexOf(c);
            result = result > index || result == -1 ? index : result;
        }

        return result;
    }
```

