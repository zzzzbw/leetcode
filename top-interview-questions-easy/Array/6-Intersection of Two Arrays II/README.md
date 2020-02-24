# Intersection of Two Arrays II

## 原题

[Intersection of Two Arrays II](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/674/)

Given two arrays, write a function to compute their intersection.

**Example:**
Given *nums1* = `[1, 2, 2, 1]`, *nums2* = `[2, 2]`, return `[2, 2]`.

**Note:**

- Each element in the result should appear as many times as it shows in both arrays.
- The result can be in any order.

**Follow up:**

- What if the given array is already sorted? How would you optimize your algorithm?
- What if *nums1*'s size is small compared to *nums2*'s size? Which algorithm is better?
- What if elements of *nums2* are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

## 解题

题目意思就是有两个数组，找出两个数组的交集

### 方法1

最简单的就是用ArrayList把nums1存起来，然后遍历nums2查看numlist1中有没有，如果有存入result中并remove掉。这种算法不好就是list1.contains()用的是遍历查找,耗时太久。

```java
	// 时间复杂度高O(mn)
	public int[] intersect(int[] nums1, int[] nums2) {
        List<Integer> list1 = new ArrayList<>();
        for (int i : nums1) {
            list1.add(i);
        }
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < nums2.length; i++) {
            if (list1.contains(nums2[i])) { // ArrayList的contains时间复杂度为nums2.length
                result.add(nums2[i]);
                list1.remove(new Integer(nums2[i]));
            }
        }
        int[] res = new int[result.size()];
        for (int i = 0; i < result.size(); i++) {
            res[i] = result.get(i);
        }
        return res;
    }
```

### 方法2

由于方法1中ArrayList.contains()耗时太久，所以就可以考虑用Hash来做。由于要考虑数组中重复数字的情况，所以用HashMap,其中key存储数组的数，value存储这个数再在数组中出现的次数。

```java
	// 时间复杂度O(m+n)
    public int[] intersect(int[] nums1, int[] nums2) {
        List<Integer> result = new ArrayList<>();
        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums1.length; i++) {
            if (map.containsKey(nums1[i])) {
                map.put(nums1[i], map.get(nums1[i]) + 1);
            } else {
                map.put(nums1[i], 1);
            }
        }

        for (int i : nums2) {
            if (map.containsKey(i)) {
                result.add(i);
                if (map.get(i).equals(1)) {
                    map.remove(new Integer(i));
                } else {
                    map.put(i, map.get(i) - 1);
                }
            }
        }

        int[] res = new int[result.size()];
        for (int i = 0; i < result.size(); i++) {
            res[i] = result.get(i);
        }
        return res;
    }
```

### 方法3

排序+双指针法。先把两个数组排序，然后设置两个指针分别指向两个数组的第一位。如果相同，则两个同时进1，否则数组数小的向前进1。这种算法时间复杂度主要取决于使用的排序算法。这种算法消耗空间最小

```java
	// 时间复杂度O(nlogn+mlogm)
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);// java底层采用DualPivotQuicksort快速排序O(nlog(n))
        Arrays.sort(nums2);
        List<Integer> result = new ArrayList<>();
        int len1 = 0;
        int len2 = 0;
        while (len1 < nums1.length && len2 < nums2.length) {
            if (nums1[len1] == nums2[len2]) {
                result.add(nums1[len1]);
                len1++;
                len2++;
            } else if (nums1[len1] > nums2[len2]) {
                len2++;
            } else {
                len1++;
            }

        }

        int[] res = new int[result.size()];
        for (int i = 0; i < result.size(); i++) {
            res[i] = result.get(i);
        }
        return res;
    }
```

### Follow up

1:如果数组已经排序了，哪个算法好。

必然是方法3了，还省去了排序的时间

2.如果数组1小于数组2，哪个算法好

用方法2，将数组1放入hashmap中

3.如果数组2太大不能全部读进内存时，应该怎么办

用方法2，将数组1放入hashmap中，然后分批读取数组2，直到hashmap中数据读完或者数组2读完。