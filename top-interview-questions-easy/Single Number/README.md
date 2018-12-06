# Single Number

## 原题

[Single Number](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/549/)

Given an array of integers, every element appears *twice* except for one. Find that single one.

**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## 解题

题目意思就是有个数组中所有数字都是有两个的，只有一个数字是单个的，找出这个数字。

### 方法1

自己想到的有两个方法，一个就是双重循环遍历每个数字找到其另一个相同的数字，这种时间复杂度是O(n^2)。另一个就是先排序，然后循环查找相邻两个是否一样，这种时间复杂度由排序算法决定。

后来网上看到一个**O(n)**的算法，就是**利用XOR运算**。

由于A XOR A = 0 且 ((A^A) ^ (B^B) ^ (C^C) ^ (D^D) ^ E) = ((0^ 0 ^ 0 ^ 0 ^ E) =E

所以只需要把整个数组都做异或运算最后的结果就是单个的数字。

```java
public int singleNumber(int[] nums) {
        if (nums.length <= 1) {
            return nums[0];
        }
        int single = 0;
        for (int i : nums) {
            single = single ^ i;
        }
        return single;
}
```

