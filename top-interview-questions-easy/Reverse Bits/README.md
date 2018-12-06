# Reverse Bits

## 原题

[Reverse Bits ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/648/)

Reverse bits of a given 32 bits unsigned integer.

**Example:**

```
Input: 43261596
Output: 964176192
Explanation: 43261596 represented in binary as 00000010100101000001111010011100, 
             return 964176192 represented in binary as 00111001011110000010100101000000.
```

**Follow up**:
If this function is called many times, how would you optimize it?

## 解题

这题意思是把一个数在二进制下反转过来

### 方法1

这题的思路其实和[Number of 1 Bits](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/565/)差不多，原数字向右移位的同时将新数字向左移位，同时判断原数字当前位是否为1，如果是1就在新数字当前位加一

```java
public int reverseBits(int n) {
	int result = 0;
	for (int i = 0; i < 32; i++) {
		result = result << 1;
		result += n & 1;
		n = n >> 1;
	}
	return result;
}
```

