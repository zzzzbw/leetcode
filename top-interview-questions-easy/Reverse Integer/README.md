# Reverse Integer

## 原题

[Reverse Integer](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/880/)

Given a 32-bit signed integer, reverse digits of an integer.

**Example 1:**

```
Input: 123
Output:  321
```

**Example 2:**

```
Input: -123
Output: -321
```

**Example 3:**

```
Input: 120
Output: 21
```

**Note:**
Assume we are dealing with an environment which could only hold integers within the 32-bit signed integer range. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

## 解题

题目意思就是翻转int型的数字。当翻转后的数字溢出时，则返回0

### 方法1

这个方法主要是分两步

1.翻转数字：把数字转化为字符串，然后翻转。

2.判断是否溢出，先比较前9位是否大于等于‘214748364’，然后再比较最后一位，如果是负数则和'8'比较，如果是正数则和'7'比较

```java
public int reverse(int x) {
        boolean isNegative = x < 0 ? true : false;
        String s = String.valueOf(x);
        char[] cs = isNegative ? s.substring(1).toCharArray() : s.toCharArray();

        int n = cs.length - 1;
        for (int i = 0; i < (n + 1) / 2; i++) {
            cs[i] = (char) (cs[i] ^ cs[n - i]);
            cs[n - i] = (char) (cs[n - i] ^ cs[i]);
            cs[i] = (char) (cs[i] ^ cs[n - i]);
        }

        if (cs.length == 10) {
            int max = 214748364;
            int num = Integer.valueOf(new String(cs, 0, 9));
            if (num > max) {
                return 0;
            } else if (num == max) {
                boolean overflow = (isNegative && cs[9] > '8') || (!isNegative && cs[9] > '7');
                if (overflow) {
                    return 0;
                }
            }
        }
        if (isNegative) {
            return -Integer.valueOf(new String(cs));
        }
        return Integer.valueOf(new String(cs));
    }
```

### 方法2

1.循环对数字取10的余数，然后乘10，实现翻转

2.用long型存储结果，这样可以直接比较大小判断是否溢出。

```java
 	public int reverse(int x) {
        long res = 0l;
        while (x != 0) {
            res = res * 10 + x % 10;
            x /= 10;
        }

        return (int) ((res > Integer.MAX_VALUE || res < Integer.MIN_VALUE) ? 0 : res);
    }
```

### 方法3

翻转和方法2相同。

用int型存储结果，在乘10的时候比较乘之前和乘之后再除以10的数字，如果是溢出的那么这两个就不一样了。

```java
	public int reverse(int x) {
        int res = 0;
        while (x != 0) {
            int temp = res * 10 + x % 10;
            x /= 10;
            if (temp / 10 != res) {
                return 0;
            }
            res = temp;
        }
        return res;
    }
```

