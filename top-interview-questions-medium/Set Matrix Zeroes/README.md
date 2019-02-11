# Set Matrix Zeroes 

## 原题

[Set Matrix Zeroes ](https://leetcode.com/explore/interview/card/top-interview-questions-medium/103/array-and-strings/777/)

Given a *m* x *n* matrix, if an element is 0, set its entire row and column to 0. Do it [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm).

**Example 1:**

```
Input: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
Output: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

**Example 2:**

```
Input: 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
Output: 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```

**Follow up:**

- A straight forward solution using O(*m**n*) space is probably a bad idea.
- A simple improvement uses O(*m* + *n*) space, but still not the best solution.
- Could you devise a constant space solution?

## 解题

题目的意思就是给一个m * n的矩阵，假如某一个元素为0，则使该元素所在的行和列都变为0

### 方法1-复制修改（暴力法）

一开始想要直接一边遍历矩阵一边把查找到0的元素的行列都变成0，但是这样是不行的。因为这样遍历的同时设置一个元素的行列为0，那这个元素这一列后面的元素就变成0，那遍历走到下一个元素的时候就把下一个元素的行列也变成0，最后导致整个矩阵都变成0。

所以为了避免这种情况，就想复制一个矩阵出来，在新的矩阵上查找，然后修改旧的矩阵。

空间复杂度：o(mn)

```java
public void setZeroes(int[][] matrix) {
    if (matrix.length == 0 || matrix[0].length == 0) {
        return;
    }
    int[][] clone = new int[matrix.length][matrix[0].length];
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix[i].length; j++) {
            clone[i][j] = matrix[i][j];
        }
    }

    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix[i].length; j++) {
            if (clone[i][j] == 0) {
                setColZero(matrix[i]);
                setRowZero(matrix, j);
            }
        }
    }
}

private void setColZero(int[] col) {
    for (int i = 0; i < col.length; i++) {
        col[i] = 0;
    }
}

private void setRowZero(int[][] row, int col) {
    for (int i = 0; i < row.length; i++) {
        row[i][col] = 0;
    }
}
```

### 方法2-行列标记

方法1复制了整个矩阵来遍历，空间复杂度就为o(mn)了。实际上没必要复制整个矩阵，因为当某个元素为0的时候，设置这个元素的行列为0，那么实际上只需要知道这个元素的行和列所在的位置就行了。所以这次用两个数组分别记录某个行或者某个列为0的位置，空间复杂度就降为o(max(m,n))。

空间复杂度：o(max(m,n))

```java
public void setZeroes(int[][] matrix) {
    if (matrix.length == 0 || matrix[0].length == 0) {
        return;
    }
    boolean[] colZero = new boolean[matrix.length];
    boolean[] rowZero = new boolean[matrix[0].length];
    for (int i = 0; i < matrix.length; i++) {
        for (int j = 0; j < matrix[i].length; j++) {
            if (matrix[i][j] == 0) {
                colZero[i] = true;
                rowZero[j] = true;
            }
        }
    }
    for (int i = 0; i < colZero.length; i++) {
        if (colZero[i]) {
            setColZero(matrix[i]);
        }
    }
    for (int i = 0; i < rowZero.length; i++) {
        if (rowZero[i]) {
            setRowZero(matrix, i);
        }
    }
}

private void setColZero(int[] col) {
    for (int i = 0; i < col.length; i++) {
        col[i] = 0;
    }
}

private void setRowZero(int[][] row, int col) {
    for (int i = 0; i < row.length; i++) {
        row[i][col] = 0;
    }
}
```

### 方法3-首位标记

方法2用了两个数组分别标记每行和每列0的位置，如果想要进一步优化，就不需要这两个数组。只要利用原来矩阵的首行和首列来代替这两个数组，作为每行或每列0的位置的标记。然后再另外用两个bool值来记录首行和首列是否有0。这样空间复杂度只有o(1)。

```java
public void setZeroes(int[][] matrix) {
    if (matrix == null || matrix.length == 0 || matrix[0].length == 0)
        return;
    boolean rowFlag = false;
    boolean colFlag = false;
    for (int i = 0; i < matrix.length; i++) {
        if (matrix[i][0] == 0) {
            colFlag = true;
            break;
        }
    }
    for (int i = 0; i < matrix[0].length; i++) {
        if (matrix[0][i] == 0) {
            rowFlag = true;
            break;
        }
    }
    for (int i = 1; i < matrix.length; i++) {
        for (int j = 1; j < matrix[0].length; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0;
                matrix[0][j] = 0;
            }
        }
    }
    for (int i = 1; i < matrix.length; i++) {
        for (int j = 1; j < matrix[0].length; j++) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0)
                matrix[i][j] = 0;
        }
    }
    if (colFlag) {
        for (int i = 0; i < matrix.length; i++) {
            matrix[i][0] = 0;
        }
    }
    if (rowFlag) {
        for (int i = 0; i < matrix[0].length; i++) {
            matrix[0][i] = 0;
        }
    }
}
```






