# Missing Number

## 原题

[Missing Number](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/722/)

Given an array containing *n* distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Example 1:**

```
Input: [3,0,1]
Output: 2
```

**Example 2:**

```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

**Note**:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

## 解题

这题的意思就是有个数组，里面的数是无需的0到n，但是缺少了一个数，要你找出缺少的数。并且要求时间复杂度为O(n),空间复杂度为1。

### 方法1

由于数组中是0到n的数少一个，那么可以先计算出0到n之和的大小，然后减去该数组总和的大小就是缺少的数。0到n之和用等差数列公式求出即可。

```java
public int missingNumber(int[] nums) {
    int len = nums.length, sum = 0;
    int total = (len + 1) * len / 2;
    for (int i = 0; i < len; i++) {
        sum += nums[i];
    }
    return total - sum;
}
```

### 方法2

和方法一有点类似，只是用了异或的方法。只要把数组里的数全部和完整的0到n的数进行异或，那么最后的值就是在数组中没有的。

```java
public int missingNumber(int[] nums) {
    int res = 0;
    for (int i = 0; i < nums.length; i++) {
        res ^= (i + 1) ^ nums[i];
    }
    return res;
}
```

