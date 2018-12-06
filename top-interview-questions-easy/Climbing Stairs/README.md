# Climbing Stairs 

## 原题

[Climbing Stairs ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/97/dynamic-programming/569/)

You are climbing a stair case. It takes *n* steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Note:** Given *n* will be a positive integer.

**Example 1:**

```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```

**Example 2:**

```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

## 解题

就是爬楼梯的问题。上楼梯的时候可以一次上一格也可以一次上两个，问上一个n层的楼梯一共有几种方式。

### 方法1--斐波那契数列解法(利用缓存)

该题目为动态规划题。通过倒推思路，要到达第n台阶，必然从n-1台阶上去或者n-2台阶上去，那么到第n台阶的方法就有到n-1台阶方法数量+到n-2台阶方法数量。即得到公式f(n) = f(n-1) + f(n-2)，这个公式实际上就是斐波那契数列。这个方法是可以获取正确答案的，只是在leetcode会用时过长异常。

所以就利用一个HashMap作为缓存，存储n->f(n)的键值对，这样在递归计算斐波那契数列的时候，以往算过的值就可以直接在缓存中获取，不必再次递归计算了。

```java
private static final Map<Integer, Integer> cache = new HashMap<>(4);

public int climbStairs(int n) {
    if (n <= 3) {
        return n;
    }
    Integer x = cache.get(n - 1);
    if (null == x) {
        x = climbStairs(n - 1);
        cache.put(n - 1, x);
    }
    Integer y = cache.get(n - 2);
    if (null == y) {
        y = climbStairs(n - 2);
        cache.put(n - 2, y);
    }
    return x + y;
}
```

### 方法2--斐波那契数列解法(循环实现)

利用循环来实现斐波那契数列，这种解更优。

```java
public int climbStairs(int n) {
	if (n <= 3) {
		return n;
	}
	int result = 0;
	int pre = 1;
	for (int i = 0; i <= n; i++) {
		int temp = result;
		result = result + pre;
		pre = temp;
	}
	return result;
}
```

