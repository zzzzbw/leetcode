# Hamming Distance

## 原题

[Hamming Distance](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/762/)

Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

The [Hamming distance](https://en.wikipedia.org/wiki/Hamming_distance) between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x` and `y`, calculate the Hamming distance.

**Note:**
0 ≤ `x`, `y` < 231.

**Example:**

```
Input: x = 1, y = 4

Output: 2

Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑

The above arrows point to positions where the corresponding bits are different.
```

## 解题

这题就是比较x和y在二进制下有多少位不一样

### 方法1

这题的思路其实和[Number of 1 Bits](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/565/)差不多，只不过这题是两个数之间的二进制比较，`Number of 1 Bits`是一个数有多少个二进制，但事实上都是通过位运算获取每一位是1还是0，然后通过移位运算符实现‘除以2’的效果。

```java
public int hammingDistance(int x, int y) {
    int count = 0;
    for (int i = 0; i < 31; i++) {
        if ((x & 1) != (y & 1))
            count++;
        x = x >> 1;
        y = y >> 1;
    }

    return count;
}
```

