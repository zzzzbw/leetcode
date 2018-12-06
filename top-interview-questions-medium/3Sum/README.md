# 3Sum

## 原题

[3Sum](https://leetcode.com/explore/interview/card/top-interview-questions-medium/103/array-and-strings/776/)

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

## 解题

题目意思是从数组中获取三个数字，这三个数和为零

### 方法1-排序指针

和2sum的题目类似，2sum里面是两个数相加，现在要3个数字，那么就先固定一个数字，剩下的两个数加起来为固定的数字的相反数就好了，分解一下实际上也就是2sum。先把数组排序，然后从第一个数开始作为固定的数，剩下两个数为固定数i+1和最后一个数，由于数组已经排序过，如果这三个数和大于0，那么最后数向前移一位，如果小于0，那么i+1再向前移动一位。直到和为0或者左边数的位置大于右边数了。 但是要注意的问题就是不要有重复的结果。

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> list = new ArrayList<>();
    if (nums.length < 3) {
        return list;
    }
    Arrays.sort(nums);
    for (int i = 0; i < nums.length - 2; i++) {
        if (i != 0 && nums[i] == nums[i - 1])
            continue;
        int left = i + 1, right = nums.length - 1;
        while (left < right) {
            int result = nums[i] + nums[left] + nums[right];
            if (result == 0) {
                List<Integer> l = Arrays.asList(nums[i], nums[left], nums[right]);
                list.add(l);
                // 不能直接right++，要去除重复的数字
                while (nums[right] == nums[--right] && left < right)
                    ;
                // 不能直接left--，要去除重复的数字
                while (nums[left] == nums[++left] && left < right)
                    ;
            } else if (result > 0) {
                right--;
            } else {
                left++;
            }
        }
    }
    return list;
}
```



