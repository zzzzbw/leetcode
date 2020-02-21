# Remove Duplicates from Sorted Array

## 原题

[Remove Duplicates from Sorted Array](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/727/)

Given a sorted array, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

**Example:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the new length.
```

## 解题

题目意思就是去除**排序好**的数组中重复的数字，并且额外的空间复杂度为O(1)

### 方法1

一开始想到的方法就是双重循环遍历数组，如果有相同的，就将该数字移除(`nums[i]=nums[i+1]`）

```java
	public int removeDuplicates(int[] nums) {
        if (nums.length <= 1) {
            return nums.length;
        }
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            int key = nums[i];
            for (int j = i + 1; j < len; j++) {
                if (nums[j] == key) {
                    remove(nums, j, len);
                    len--;
                    j--; //注意由于当前数字被覆盖,要j--再次判断当前j的数字
                }
            }
        }
        return len;
    }

    private void remove(int[] nums, int index, int len) {
        for (int i = index; i < len - 1; i++) {
            nums[i] = nums[i + 1];
        }
    }
```

### 方法2

用双重指针，由于该数组队列已经是排序过的，所以重复的数字必定都是靠在一起的。设置一个慢指针和一个快指针。当慢指针指向的数字和快指针一样的时候，慢指针不动，快指针像前一步。当两个不一样的时候，慢指针向前一步，然后这时候再与快指针指向的交换。直到快指针到数组的最后，慢指针的长度+1就是不重复数组的长度。

```java
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0) {
            return 0;
        }
        if (nums.length == 1) {
            return 1;
        }
        int slow = 0;
        int fast = 1;
        int key;
        while (fast < nums.length) {
            key = nums[slow];
            if (key != nums[fast]) {
                slow++;
                nums[slow] = nums[fast];
                fast++;
            } else {
                fast++;
            }
        }
        return slow + 1;
    }
```

### 方法3

原理和方法2一样，不过更加简洁好理解。先利用一个变量从1开始记录当前指针的位置，然后遍历数组，如果当前数和前一个数不一样，说明这是“第一个”不重复的数，就把该数移到当前指针的位置，并把指针向后移一位。

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0 || nums.length == 1) {
        return nums.length;
    }

    int current = 1; // 当前指针位置
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] != nums[i - 1]) {
            nums[current] = nums[i];
            current++;
        }
    }

    return current;
}
```

