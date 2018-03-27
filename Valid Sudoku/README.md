# Valid Sudoku

## 原题

[Valid Sudoku](https://leetcode.com/explore/interview/card/top-interview-questions-easy/92/array/769/)

Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

The Sudoku board could be partially filled, where empty cells are filled with the character `'.'`.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png)

A partially filled sudoku which is valid.

**Note:**
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

## 解题

题目意思就是根据数独的规则检验这个矩阵。即每行9个，每列9个，和每个9宫格的9个数字不能重复。

### 方法1

其实就是双重循环分别检验每行，每列，每个9宫格的数字。比较费心的就是9宫格的行和列的计算。

```java
    //时间复杂度o(n^2)
	public boolean isValidSudoku(char[][] board) {
        Set<Integer> row = null;
        Set<Integer> col = null;
        Set<Integer> table = null;
        for (int i = 0; i < board.length; i++) {
            row = new HashSet<>();
            col = new HashSet<>();
            table = new HashSet<>();

            for (int j = 0; j < board[i].length; j++) {
                // 第i行
                if (board[i][j] != '.' && !row.add(new Integer(board[i][j]))) {
                    return false;
                }
                // 第i列
                if (board[j][i] != '.' && !col.add(new Integer(board[j][i]))) {
                    return false;
                }

                int tableRow = 3 * (i / 3) + j / 3;
                int tableCol = 3 * (i % 3) + j % 3;
                if (board[tableRow][tableCol] != '.'
                        && !table.add(new Integer(board[tableRow][tableCol]))) {
                    return false;
                }
            }
        }
        return true;
    }
```
