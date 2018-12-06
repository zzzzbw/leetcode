# Maximum Subarray 

## 原题

[Maximum Subarray  ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/97/dynamic-programming/566/)

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

**Example:**

```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

**Follow up:**

If you have figured out the O(*n*) solution, try coding another solution using the divide and conquer approach, which is more subtle.

## 解题

这题就是获取最大子数组。(leetcode建议可以使用分治法，这里暂时不用了)

### 方法1-动态规划

这个方法就是动态规划法，通过变量`result`存储最终结果和`temp`存储左边最大子数组的和来实现。关键思路就是`temp = Math.max(temp + num, num)`这一步，当该数组其左边的最大子数组+当前num还没当前num大，说明此时左边的最大子数组为num。以此类推就能获得最大子数组

```java
public int maxSubArray(int[] nums) {
    int result = Integer.MIN_VALUE;
    int temp = 0;
    for (int num : nums) {
        temp = Math.max(temp + num, num);
        result = Math.max(result, temp);
    }

    return result;
}
```
