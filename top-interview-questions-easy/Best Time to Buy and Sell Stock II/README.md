# Best Time to Buy and Sell Stock II

## 原题

[Best Time to Buy and Sell Stock II](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/564/)

Say you have an array for which the *i*th element is the price of a given stock on day *i*.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).



## 解题

题目意思就是有个长度为i的数组，数组中每个位置代表的是每天股票的价格，在不限制交易次数的情况下，获取最大的利润。

### 方法1

由于可以任意交易次数，为了获取最大利润，对于一个上升子序列，比如序列[5,6,10,15,1,4]中[5,6,10,15]这个子序列，有两种操作：

1:(6-5)+(10-6)+(15-10)=10

2:15-5=10

这两种最后获得的利润一样是最大化的，所以只要遍历数组，当所有prices[i+1]>prices[i]的时候，计算差额然后加入总利润即可。这种方法为**贪心法**

```java
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int i = 0; i < prices.length - 1; i++) {
            if (prices[i] < prices[i + 1]) {
                profit += prices[i + 1] - prices[i];
            }
        }
        return profit;
    }
```

