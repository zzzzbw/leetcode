Plus One

## 原题

[Plus One](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/559/)

Given a non-negative integer represented as a **non-empty** array of digits, plus one to the integer.

You may assume the integer do not contain any leading zero, except the number 0 itself.

The digits are stored such that the most significant digit is at the head of the list.

## 解题

题目意思就是有个非负整数，每一位都是数组的一个数字，然后将这个数加一。简单来说就是大数加法。

### 方法1

这题其实很简单，就是最后一个数加一，然后处理好进位。如果没有进位就停止循环。要注意的就是假如第一位也进位了，就要new一个新的数组。

```java
	public int[] plusOne(int[] digits) {
        boolean flag = true;
        for (int i = digits.length - 1; i >= 0 && flag; i--) {
            digits[i]++;
            if (digits[i] >= 10) {
                digits[i] = digits[i] - 10;
            } else {
                flag = false;
            }
        }

        if (flag) {
            // 如果遍历完还需要进制，则说明这个数为100...的形式，那只要new一个相应长度空的int数组并设置第一位为1，其他为即是0
            int[] result = new int[digits.length + 1];
            result[0] = 1;
            return result;
        } else {
            return digits;
        }
    }
```

