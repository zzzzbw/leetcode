# Shuffle an Array 

## 原题

[Shuffle an Array ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/98/design/670/)

Shuffle a set of numbers without duplicates.

**Example:**

```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```

## 解题

题目要求设计一个类，有两个方法`reset()`和`shuffle()`，以及构造方法`Solution(nums)`。`reset()`方法返回最初传入的nums数组，`shuffle()`返回打乱顺序的nums数组，且每次乱序的概率相同。

### 方法1-随机取

题目主要实现的就是shuffle()方法。要返回一个打乱的数组，可以先新建一个空的数组，然后为了防止打乱原数组，再nums.clone()一个数组copy，接着每次都从copy数组中随机取一个数放到空数组中，就是一个乱序数组了。为了防止在copy数组中取到已经取过的数，每次随机的长度都用数组剩余数的数量，然后取了之后再把copy数组当前最后一位数补到取出的数的位置。

```java
class Solution {
    private int[] nums;
	private Random rand;
    
    public Solution(int[] nums) {
        this.nums = nums;
		rand = new Random();
    }
	
	public int[] reset() {
		return nums;
	}

	public int[] shuffle() {
		int[] copy = nums.clone();
		int maxlen = copy.length - 1;
		int[] result = new int[copy.length];
		for (int i = 0; i < copy.length; i++) {
			int index = rand.nextInt(maxlen + 1);
			result[i] = copy[index];
			copy[index] = copy[maxlen];
			maxlen--;
		}

		return result;
	}
}
```

### 方法2-洗牌法

洗牌法其实和上面随机取类似，只不过这是从数组前面开始交换，更简单直接一点
1. 将第1个元素和后面n个元素随机一个交换(包括自己)，这时第一个元素就确定了

2. 将第2个元素和后面n-1个元素随机一个交换(包括自己)，这时第二个元素就确定了

3. 循环直到最后一个元素

```java
public class Solution {
    private int[] original;
    private Random rng = new Random();
    private int[] copy;
    private int num;
    public Solution(int[] nums) {
        original = nums;
        copy=original.clone();
        num=original.length;
    }
    
    public int[] reset() {
        return original;
    }
    
    public int[] shuffle() {
        int n = num;
        while(n>1) {
            n--;
            int k = rng.nextInt(n + 1);
            int value = copy[k];
            copy[k] = copy[n];
            copy[n] = value;
        }
        return copy;
    }
}
```



