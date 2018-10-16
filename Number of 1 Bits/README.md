# Number of 1 Bits 

## 原题

[Number of 1 Bits](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/565/)

Write a function that takes an unsigned integer and returns the number of '1' bits it has (also known as the [Hamming weight](http://en.wikipedia.org/wiki/Hamming_weight)).

**Example 1:**

```
Input: 11
Output: 3
Explanation: Integer 11 has binary representation 00000000000000000000000000001011 
```

**Example 2:**

```
Input: 128
Output: 1
Explanation: Integer 128 has binary representation 00000000000000000000000010000000
```

## 解题

这题就是获得一个int类型的数字的2进制下有多少个1

### 方法1

这题一开始我想很简单啊，只要不停的取余这个数不就行了吗。但是提交之后却报错了，因为题目有个提示是`/you need to treat n as an unsigned value`,意思就是这个数是无符号的数。在java中int型是有符号的数，其为32位的，最高位是符号位，所以能表达2^31~-2^31的数。现在要表达无符号的数，即0~2^32位，就不能用取余的方法了。

而是应该用按位与（&）运算，因为在计算机中负数实际上已补码的形式表现，比如32位的-2147483648原码是01111111111111111111111111111111,那么其补码就是10000000000000000000000000000001，这个补码和32无符号位的数字2147483648是相同的，因为正数的补码也就是其本身，所以用位运算的话就不用考虑这个数有没有符号位了，因为都是按无符号来算。

```java
public int hammingWeight(int n) {
    int res = 0;
    for (int i = 0; i < 32; ++i) {
        res += (n & 1);
        n = n >> 1;
    }
    return res;
}
```




