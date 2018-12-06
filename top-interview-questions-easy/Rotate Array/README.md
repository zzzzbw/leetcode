# Rotate Array

## 原题

[Rotate Array](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/646/)

Rotate an array of n elements to the right by k steps.

For example, with n = 7 and k = 3, the array `[1,2,3,4,5,6,7]` is rotated to `[5,6,7,1,2,3,4]`.

Note:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.

Hint:
Could you do it in-place with O(1) extra space?
Related problem: Reverse Words in a String II

Credits:
Special thanks to @Freezen for adding this problem and creating all test cases.

## 解题

题目意思就是给定一个数组,给定一个位置n,从该位置'旋转改数组'。并且额外消耗空间为O(1)。

### 方法1

思路就是从位置n把数组分为两部分，分别倒过来，然后将新的数组倒过来。
如：
1,2,3,4,5,6,7 n=3

第一次:**3,2,1,**4,5,6,7
第二次:3,2,1,**7,6,5,4**
第三次:**4,5,6,7,1,2,3**

另外要注意的是题目中没有提到，就是当n大于数组的长度的时候，不是直接return，而是取余n，然后再对数组'旋转'
```java
	public void rotate(int[] nums, int k) {
        int n = nums.length;
        if (n <= 1 || k == 0 || k == n) {
            return;
        }
        k = k % n;
        swap(nums, 0, n - k - 1);
        swap(nums, n - k, n - 1);
        swap(nums, 0, n - 1);
    }

    public void swap(int[] nums, int start, int end) {
        int n = ((end - start) / 2) + 1;
        int step = end - start;
        for (int i = 0; i < n; i++) {
            int temp = nums[i + start];
            nums[i + start] = nums[i + start + step];
            nums[i + start + step] = temp;
            step -= 2;
        }
    }
```


