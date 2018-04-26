# Merge Sorted Array

## 原题

[Merge Sorted Array](https://leetcode.com/explore/interview/card/top-interview-questions-easy/96/sorting-and-searching/587/)

Given two sorted integer arrays *nums1* and *nums2*, merge *nums2* into *nums1* as one sorted array.

**Note:**

- The number of elements initialized in *nums1* and *nums2* are *m* and *n* respectively.
- You may assume that *nums1* has enough space (size that is greater or equal to *m* + *n*) to hold additional elements from *nums2*.

**Example:**

```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```

## 解题

题目的意思就是把两个有序的数组合并成一个有序数组。

### 方法1

这个方法不是很好，从头比对两个数组，假如数组1的数大，则将该数组后移一位，把数组2的数放进去。由于这个每次都要后移，所以不好

```java
	 public void merge(int[] nums1, int m, int[] nums2, int n) {
        int l1 = 0;
        int l2 = 0;
        int length = m;
        while (l1 < nums1.length && l2 < n) {
            if (nums1[l1] > nums2[l2]) {
                move(nums1, l1, length);
                nums1[l1] = nums2[l2];
                l1++;
                l2++;
                length++;
            } else {
                l1++;
            }
        }
        if (l2 < n) {
            for (int i = length; i < m + n; i++) {
                nums1[i] = nums2[l2++];
            }
        }
    }

    private void move(int[] nums, int index, int length) {
        for (int i = length; i > index; i--) {
            int temp = nums[i];
            nums[i] = nums[i - 1];
            nums[i - 1] = temp;
        }
    }
```

### 方法2

方法1每次都要后移，然而我们直接从后面开始比对，就不用后移了。比对两个数组，哪个数比较大就放在数组1的后面

```java
	public void merge(int[] nums1, int m, int[] nums2, int n) {
        int l1 = m - 1;
        int l2 = n - 1;
        int length = m + n - 1;
        while (l1 >= 0 && l2 >= 0) {
            if (nums1[l1] > nums2[l2]) {
                nums1[length--] = nums1[l1--];
            } else {
                nums1[length--] = nums2[l2--];
            }
        }
        while (l1 >= 0) {
            nums1[length--] = nums1[l1--];
        }
        while (l2 >= 0) {
            nums1[length--] = nums2[l2--];
        }
    }
```

