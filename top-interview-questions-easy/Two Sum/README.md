# Two Sum

## 原题

[Two Sum](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/546/)

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

## 解题

题目意思就是给一个数，这个数是数组中两个数之和，找出这两个数再数组中的位置

### 方法1-排序指针

先复制这数组并且排序，然后用两个指针指向数组第一和最后，当nums[small]+nums[big]>target时，big--，当nums[small]+nums[big]<target时，small++。当相等的时候small和big所指的位置就是要找的数。然后再在原数组中查找出这两个数的位置，注意处理两个数相等的情况就可以了。

```java
    //时间复杂度o(nlogn)
	public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        int[] sorts = Arrays.copyOf(nums, nums.length);
        Arrays.sort(sorts);//DualPivotQuicksort 双轴快排 时间复杂度O(nlogn)
        int small = 0;
        int big = sorts.length - 1;
        int[] temp = new int[2];
        while (small < big) {
            if (sorts[small] + sorts[big] < target) {
                small++;
            } else if (sorts[small] + sorts[big] > target) {
                big--;
            } else {
                break;
            }
        }
        temp[0] = sorts[small];
        temp[1] = sorts[big];
        boolean flag1 = false;
        boolean flag2 = false;
        for (int i = 0; i < nums.length; i++) {
            if (temp[0] == nums[i] && !flag1) {
                result[0] = i;
                flag1 = true;
            } else if (temp[1] == nums[i] && !flag2) {
                result[1] = i;
                flag2 = true;
            }
            if (flag1 && flag2) {
                break;
            }
        }
        return result;
    }
```

### 方法2.1-HashMap

利用哈希表查找key的时间为O(1),遍历数组的时候查找map中有没有key。如果没有，则保存这个数的差和index，比如nums[2]=7，target=9,则查找map中key有没有为2的，没有的话保存key=target-nums[2]，value=2。如果有，则直接通过key得到value。

```java
 	//O(n)
	public int[] twoSum2(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(nums[i])) {
                result[0] = map.get(nums[i]);
                result[1] = i;
            }

            map.put(target - nums[i], i);
        }
        return result;
    }
```

### 方法2.2-HashMap

和方法2.1类似，只是这个是直接在map中保存nums[i]，而不是target-nums[i]。这个方法相对麻烦

```java
    // O(n)
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            map.put(nums[i], i);
        }
        int key1 = 0;
        int key2 = 0;
        for (int key : map.keySet()) {
            if (map.containsKey(target - key)) {
                key1 = key;
                key2 = target - key;
                break;
            }
        }

        if (key1 == key2) {
            boolean isKey1 = false;
            for (int i = 0; i < nums.length; i++) {
                if (nums[i] == key1) {
                    if (!isKey1) {
                        result[0] = i;
                        isKey1 = true;
                    } else {
                        result[1] = i;
                        break;
                    }
                }
            }
        } else {
            result[0] = map.get(key1);
            result[1] = map.get(key2);
        }
        return result;
    }
```

