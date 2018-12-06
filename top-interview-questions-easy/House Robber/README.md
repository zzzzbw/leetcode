# House Robber

## 原题

[House Robber](https://leetcode.com/explore/interview/card/top-interview-questions-easy/97/dynamic-programming/576/)

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight **without alerting the police**.

**Example 1:**

```
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```

**Example 2:**

```
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```

## 解题

题目讲了一个强盗的故事，但实际上要我们求的是，取一列数组中的数字，每个数字不能连续，怎么取和最大。

### 方法1-动态规划

假设有这么一列十个数的数组[2, 3, 4, 1, 9, 3, 2, 3, 3, 4]，有以下思考思路

1. 假设小偷偷得顺序是按照从左往右，那么最终停止的位置只能是9或10 
2. 如果从位置10往前回溯，分别有两个可以选择的房子7和8，位置9也是一样的
3. 需要选择从左边开始到money数目最大的那个房子，那么可以看到这是一个递归的过程
4. 因为中间会有一些重复的计算，比如在求位置10的向前回溯的时候，需要计算位置7的money值，计算位置9前溯同样需要计算位置7的money，所以我们需要将已经计算过的值进行记录

这时候发现这个题目有点类似于爬楼梯了，想要获取max（位置9总和，位置10总和），那么就往前推理，只要获取max（位置10的值+位置8之前的总和，位置10+位置7之前总和）以及max（位置9的值+位置7之前的总和，位置9+位置6之前总和）的较大值。

同时为了保证性能，减少重复的计算，把之前计算过的最大值的结果保存。这里用了一个`money`数组。

```java
public int rob(int[] nums) {
    if (nums.length == 0) {
        return 0;
    }
    if (nums.length == 1) {
        return nums[0];
    }
    if (nums.length == 2) {
        return Math.max(nums[0], nums[1]);
    }

    int[] money = new int[nums.length];
    money[0] = nums[0];
    money[1] = nums[1];
    money[2] = nums[0] + nums[2];
    for (int i = 3; i < nums.length; i++) {
        money[i] = Math.max(nums[i] + money[i - 2], nums[i] + money[i - 3]);
    }

    return Math.max(money[money.length - 1], money[money.length - 2]);
}
```
