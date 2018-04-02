# Count and Say

## 原题

[Count and Say](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/886/)

The count-and-say sequence is the sequence of integers with the first five terms as following:

```
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

`1` is read off as `"one 1"` or `11`.
`11` is read off as `"two 1s"` or `21`.
`21` is read off as `"one 2`, then `one 1"` or `1211`.

Given an integer *n*, generate the *n*th term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

**Example 1:**

```
Input: 1
Output: "1"
```

**Example 2:**

```
Input: 4
Output: "1211"
```

## 解题

题目意思就是根据口语念出来这行字符串，就是下一行字符串。比如第三行是'21'，念出来就是‘1’个‘2’，’1‘个’1‘，所以第四行是’1211‘。念出来就是‘1’个‘1’，‘1’个‘2’，‘2’个‘1’，所以第五行就是111221。

### 方法1

其实就是从第一行开始根据该行的字符串计算出下一行的字符串。

```java
	public String countAndSay(int n) {
        String word = "1";
        if (n == 1) {
            return word;
        }
        for (int i = 0; i < n - 1; i++) {
            word = say(word);
        }
        return word;
    }

    private String say(String lineSay) {
        StringBuilder sBuilder = new StringBuilder();
        char number = '0';
        char count = '0';
        for (int i = 0; i < lineSay.length(); i++) {
            if (lineSay.charAt(i) == number) {
                count++;
            } else {
                if (count != '0') {
                    sBuilder.append(count).append(number);
                }
                number = lineSay.charAt(i);
                count = '1';
            }
        }
        if (count != '0') {
            sBuilder.append(count).append(number);
        }
        return sBuilder.toString();
    }
```
