# Best Time to Buy and Sell Stock 

## 原题

[Best Time to Buy and Sell Stock ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/97/dynamic-programming/572/)

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

**Example 1:**

```
Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
```

**Example 2:**

```
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```

## 解题

题目意思就是有个长度为i的数组，数组中每个位置代表的是每天股票的价格，只能交易一次（一次买入一次卖出），并且买入必须在卖出之前，获取最大的利润。

### 方法1-暴力解

就是计算出全部的情况的买入卖出，得到最多利润的

```java
public int maxProfit(int[] prices) {
    if (prices.length < 2) {
        return 0;
    }
    int max = 0;
    for (int i = 0; i < prices.length - 1; i++) {
        for (int j = i + 1; j < prices.length; j++) {
            if (prices[j] - prices[i] > max) {
                max = prices[j] - prices[i];
            }
        }
    }
    return max;
}
```

### 方法2

分析题目，实际上不用计算出全部的买入卖出情况。因为必须先买入再卖出，所以小的值（买入值）必须在大的值（卖出值）左边。那么只要先找到左边（相对）最小的值，然后再用在其右边的值减去这个最小值，这之中最大的值就是最大利润

```java
public int maxProfit(int[] prices) {
    int minprice = Integer.MAX_VALUE;
    int max = 0;
    for (int i = 0; i < prices.length; i++) {
        if (prices[i] < minprice) {
            minprice = prices[i];
        } else if (prices[i] - minprice > max) {
            max = prices[i] - minprice;
        }
    }
    return max;
}
```

