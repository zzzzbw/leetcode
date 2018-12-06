# Valid Anagram

## 原题

[Valid Anagram](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/882/)

Given two strings *s* and *t*, write a function to determine if *t* is an anagram of *s*.

For example,
*s* = "anagram", *t* = "nagaram", return true.
*s* = "rat", *t* = "car", return false.

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

## 解题

题目意思就是s和t是两个字符串，判断这两个字符串除了字符的顺序以外，是不是相等的。

### 方法1

判断出现次数最先想到的就是用HashMap，key存储字符，value存储出现次数，最后比较两个map里的数据是否一样。不过这种算法时间和空间复杂度都很高。

```java
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        char[] ss = s.toCharArray();
        char[] ts = t.toCharArray();
        Map<Character, Integer> sMap = new HashMap<>();
        Map<Character, Integer> tMap = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            if (null != sMap.get(ss[i])) {
                sMap.put(ss[i], sMap.get(ss[i]) + 1);
            } else {
                sMap.put(ss[i], 1);
            }
            if (null != tMap.get(ts[i])) {
                tMap.put(ts[i], tMap.get(ts[i]) + 1);
            } else {
                tMap.put(ts[i], 1);
            }
        }
        for (char c : sMap.keySet()) {
            if (null == tMap.get(c)) {
                return false;
            }

            if (!sMap.get(c).equals(tMap.get(c))) {
                return false;
            }
        }
        return true;
    }
```

### 方法2

和方法1思路类似，只是由于这个字符串中只有小写字母，所以用一个长度为26的数组分别存储每个字母出现的次数，如果s出现则+1，如果t出现则-1，最后如果整个数组都是0，表示两个字符串相等。

```java
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        char[] ss = s.toCharArray();
        char[] ts = t.toCharArray();
        int[] count = new int[26];
        for (int i = 0; i < ss.length; i++) {
            int index = ss[i] - 'a';
            count[index]++;
            index = ts[i] - 'a';
            count[index]--;
        }
        for (int i = 0; i < 26; i++) {
            if (count[i] != 0) {
                return false;
            }
        }
        return true;
    }
```

### 方法3

把两个字符串排序，这时候这两个字符串就相同了

```java
	public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }
        char[] ss = s.toCharArray();
        char[] ts = t.toCharArray();
        Arrays.sort(ss);
        Arrays.sort(ts);
        for (int i = 0; i < ss.length; i++) {
            if (ss[i] != ts[i]) {
                return false;
            }
        }
        return true;
    }
```

