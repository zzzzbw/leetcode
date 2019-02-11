# Group Anagrams 

## 原题

[Group Anagrams](https://leetcode.com/explore/interview/card/top-interview-questions-medium/103/array-and-strings/778/)

Given an array of strings, group anagrams together.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Note:**

- All inputs will be in lowercase.
- The order of your output does not matter.

## 解题

题目的意思就是给一个字符串数组，把这些字符串按照字母相同的分类。即只要两个字符串的字母是相同的，那就把这两个字符串分为一组。

### 方法1

这个方法就是遍历字符串数组，然后获取到每个字符串的`CharArray`，再将其排序，这样所有字母相同顺序不同的字符串此时也相同了。此时再进行比较归类。另外注意这里用了一个HashMap来缓存每一个归类的‘有序字符串’及其对应的list，提升查找效率。

```java
public List<List<String>> groupAnagrams(String[] strs) {
    if (strs.length == 0) {
        return Collections.emptyList();
    }
    Map<String, List<String>> cache = new HashMap<>();
    for (String str : strs) {
        char[] cs = str.toCharArray();
        Arrays.sort(cs);
        List<String> list = cache.get(new String(cs));
        if (null != list) {
            list.add(str);
        } else {
            list = new ArrayList<>();
            list.add(str);
            cache.put(new String(cs), list);
        }
    }
    return new ArrayList<>(cache.values());
}
```






