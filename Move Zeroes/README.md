# Move Zeroes

## 原题

[Move Zeroes](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/567/)

Given an array `nums`, write a function to move all `0`'s to the end of it while maintaining the relative order of the non-zero elements.

For example, given `nums = [0, 1, 0, 3, 12]`, after calling your function, `nums` should be `[1, 3, 12, 0, 0]`.

**Note**:

1. You must do this **in-place** without making a copy of the array.
2. Minimize the total number of operations.

## 解题

题目意思就是在其他数字顺序不变的情况下，把所有0都放在数组最后。不能复制一个数组出来而且尽可能少的操作数组。

### 方法1

最直接想到的方法就是循环遍历数组，如果是0的话就把数往前移动一位。这种方法消耗时间比较大

```java
// 时间复杂度O(n^2)
public void moveZeroes1(int[] nums) {
	int count = 0;
	int index = 0;
	while (index < nums.length - count) {
		if (nums[index] == 0) {
			count++;
			for (int j = index; j < nums.length - count; j++) {
				nums[j] = nums[j + 1];
			}
			nums[nums.length - count] = 0;
		} else {
			index++;
		}
	}
}
```

### 方法2

方法2和方法1其实思路类似，只是方法2是当num！=0时，向前移动一位，由于遍历的时候就是从前向后遍历，所以可以边遍历边移动，不像方法1要双重循环，所以这种时间复杂度就小

```java
//时间复杂度O(n)
public void moveZeroes(int[] nums) {
	int index = 0;
	for (int num : nums) {
		if (num != 0) {
			nums[index] = num;
			index++;
		}
	}
	while (index < nums.length) {
		nums[index++] = 0;
	}
}
```

