# Count Primes 

## 原题

[Count Primes ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/102/math/744/)

Count the number of prime numbers less than a non-negative number, **n**.

**Example:**

```
Input: 10
Output: 4
Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.
```

## 解题

这题的意思就是给一个数n，返回比这个数小的质数的个数。

### 方法1

这个方法虽然能返回结果，但是在leetcode上会超时
这个方法就是对每个数被比他小的质数取余，如果有能整除的，就说明这个数不是质数。同时用一个HashSet保存之前计算过的质数。
由于每个数都要循环计算，所以导致超时

```java
public int countPrimes(int n) {
    int count = 0;
    Set<Integer> primesSet = new HashSet<>();
    for (int i = 2; i < n; i++) {
        if (isPrimes(primesSet, i)) {
            count++;
            primesSet.add(i);
        }
    }

    return count;
}

private boolean isPrimes(Set<Integer> primesSet, int num) {
    for (int i : primesSet) {
        if (num % i == 0) {
            return false;
        }
    }
    return true;
}
```
### 方法2

这个方法使用了[埃拉托斯特尼筛法](https://zh.wikipedia.org/wiki/埃拉托斯特尼筛法),算法的方法就是：
比如要计算100以下的质数，那么用一个布尔型数组num[100]保存每个数是否为质数，一开始都为false，然后从2开始，将2的倍数全部设置为true可以被整除的，
此时num[100]里有一部分被标记为true了，然后找2的下一个为false的数，就是质数3，再把3的倍数全部设置为true，接着3下一个为false的就是5，以此类推直到n为止。

![](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b9/Sieve_of_Eratosthenes_animation.gif/350px-Sieve_of_Eratosthenes_animation.gif)

```java
public int countPrimes(int n) {
    int count = 0;
    boolean[] num = new boolean[n];
    for (int i = 2; i < n; i++) {
        if (num[i] == true) {
            continue;
        }
        count++;
        for (int j = i; j < n; j = j + i) {
            num[j] = true;
        }
    }
    return count;
}
```









