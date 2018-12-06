#Valid Palindrome

## 原题

[Valid Palindrome](https://leetcode.com/explore/interview/card/top-interview-questions-easy/127/strings/883/)

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,
`"A man, a plan, a canal: Panama"` is a palindrome.
`"race a car"` is *not* a palindrome.

**Note:**
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

## 解题

题目意思就是判断一个字符串是否为回文，忽略其中的特殊字符和空格。

### 方法1-双指针法

就是用两个指针一个指头一个指尾，如果遇到特殊字符就跳过，如果比较相等就small

++,big--，如果不相等就返回false。直到最后两个指针相遇。

```java
    //时间复杂度o(n/2)
	public boolean isPalindrome(String s) {
        if (s.length() == 0 || s.length() == 1) {
            return true;
        }
        char[] cs = s.toCharArray();
        int small = 0;
        int big = cs.length - 1;
        while (small < big) {
            if (!(cs[small] >= 'a' && cs[small] <= 'z') && !(cs[small] >= 'A' && cs[small] <= 'Z')
                    && !(cs[small] >= '0' && cs[small] <= '9')) {
                small++;
                continue;
            }

            if (!(cs[big] >= 'a' && cs[big] <= 'z') && !(cs[big] >= 'A' && cs[big] <= 'Z')
                    && !(cs[big] >= '0' && cs[big] <= '9')) {
                big--;
                continue;
            }

            if (Character.toLowerCase(cs[small]) == Character.toLowerCase(cs[big])) {
                small++;
                big--;
            } else {
                return false;
            }
        }
        return true;
    }
```
