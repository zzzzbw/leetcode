# Rotate Image

## 原题

[Rotate Image](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/770/)

You are given an *n* x *n* 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

**Note:**
You have to rotate the image **in-place**, which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

**Example 1:**

```
Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
```

**Example 2:**

```
Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```

## 解题

题目意思就是把这个矩阵顺时针旋转90度，且不能复制这个矩阵。

### 方法1

只要以对角线为轴翻转，再以中轴线为轴翻转，就可以将矩阵旋转90度。

1  2  3　　　 　1  **4**  **7**　　　　  **7**  4  **1**

4  5  6　-->　    **2**  5  **8**　 -->        **8**  5  **2**

7  8  9 　　　    **3**  **6**  9　　   　   **9**  6  **3**

或者反对角线为轴，再以中间水平轴旋转。

1  2  3　　　 　**1**  **4**  7　　　　  **7**  **4**  **1**

4  5  6　-->　    **2**  5  **8**　 -->        8  5  2

7  8  9 　　　    3  **6**  **9**　　   　   **9**  **6**  **3**

这两个都差不多，这里用的是第一种

```java
    // 时间复杂度O(n^2)
    public void rotate(int[][] matrix) {
        int n = matrix.length - 1;
        for (int i = 0; i < matrix.length; i++) {
            for (int j = i + 1; j < matrix[i].length; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length / 2; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[i][n - j];
                matrix[i][n - j] = temp;
            }
        }
    }
```
