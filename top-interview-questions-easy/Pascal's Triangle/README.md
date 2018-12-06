# Pascal's Triangle

## 原题

[Pascal's Triangle](https://leetcode.com/explore/interview/card/top-interview-questions-easy/99/others/601/)

![](https://upload.wikimedia.org/wikipedia/commons/0/0d/PascalTriangleAnimated2.gif)

In Pascal's triangle, each number is the sum of the two numbers directly above it.

**Example:**

```
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```

## 解题

这题的意思就是，给一个数值n，生成高度为n的“杨辉三角”

### 方法1

题目本身很简单，只要观察这个图形，发现公式：第n+1层的第n位=第n层的第n-1位+第n位，就可以了。然后每一层最左边和最右边是1.

```java
public List<List<Integer>> generate(int numRows) {
    List<List<Integer>> list = new ArrayList<>(numRows);
    for (int i = 0; i < numRows; i++) {
        List<Integer> row = new ArrayList<>(i + 1);
        for (int j = 0; j < i + 1; j++) {
            if (j == 0 || j == i) {
                row.add(1);
            } else {
                List<Integer> before = list.get(i - 1);
                int now = before.get(j - 1) + before.get(j);
                row.add(now);
            }
        }
        list.add(row);
    }
    return list;
}
```

