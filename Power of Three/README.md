# Power of Three

## 原题

[Power of Three ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/102/math/745/)

Given an integer, write a function to determine if it is a power of three.

**Example 1:**

```
Input: 27
Output: true
```

**Example 2:**

```
Input: 0
Output: false
```

**Example 3:**

```
Input: 9
Output: true
```

**Example 4:**

```
Input: 45
Output: false
```

**Follow up:**
Could you do it without using any loop / recursion?

## 解题

这题就是判断一个数是否为3的倍数，且不用循环或者递归

### 方法1-直接除

由于传入的是int型，所以这个数最大就是2^21，在这其中3的倍数最大为3^19=1162261467，所以只要看1162261467能够对n取余为0就行。注意要判断n是否大于0

```java
public boolean isPowerOfThree(int n) {
    return (n > 0 && 1162261467 % n == 0);
}
```
### 方法2-对数法

最后还有一种巧妙的方法，利用对数的换底公式来做，高中学过的换底公式为logab = logcb / logca，那么如果n是3的倍数，则log3n一定是整数，我们利用换底公式可以写为log3n = log10n / log103，现在问题就变成了判断log10n / log103是否为整数，在java中判断数字a是否为整数，我们可以用 a - int(a) == 0 来判断，参见代码如下：

```java
public boolean isPowerOfThree(int n) {
    return (int) (Math.log10(n) / Math.log10(3)) - Math.log10(n) / Math.log10(3) == 0;
}
```









