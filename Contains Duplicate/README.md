Contains Duplicate

## 原题

[Contains Duplicate](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/578/)

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

## 解题

题目意思就是查找该数组中是否有重复的数字，有就返回true，没有返回false

### 方法1

查找重复的第一反应就是用哈希表，因为哈希的查找时间为O(1),java中直接用HashSet就可以了。这种时间复杂度就是O(n)。

```java
	public boolean containsDuplicate(int[] nums) {
        int len = nums.length;
        if (len <= 1) {
            return false;
        }
        Set<Integer> set = new HashSet<>(len);
        for (int i : nums) {
            if (set.contains(i)) {
                return true;
            }
            set.add(i);
        }
        return false;
    }
```

### 方法2

先把数组排序,排序后的数组如果有相同的数字必然相邻，只要看相邻数字有没有相同的就可以了，这种时间负责度有排序算法决定。

```java
	public boolean containsDuplicate(int[] nums) {
        int len = nums.length;
        if (len <= 1) {
            return false;
        }
        sort(nums);// 排序算法,这里就不给具体代码
        for (int i = 0; i < len - 1; i++) {
            if (nums[i] == nums[i + 1]) {
                return true;
            }
        }
        return false;
    }
```

