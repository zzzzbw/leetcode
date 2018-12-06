# First Bad Version

## 原题

[First Bad Version](https://leetcode.com/explore/interview/card/top-interview-questions-easy/96/sorting-and-searching/774/)

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which will return whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

## 解题

这道题说是有一系列版本，其中有一个版本是坏的，而且后面跟着的全是坏的，给了一个API函数可以用来判定当前版本是否是坏的，让我们尽可能少的调用这个API，找出第一个坏版本。

### 方法1--二分法

由于好的版本和坏的版本是有一个明显的分界线的，所以用二分法去查找。需要注意的就是在找中间值的时候用(right+left)/2可能会溢出，所以用left + (right - left) / 2

```java
	 public int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while(left<right){
            int mid = left + (right - left) / 2;
            if (isBadVersion(mid)) right = mid;
            else left = mid + 1;
        }
        return left;
    }
```

