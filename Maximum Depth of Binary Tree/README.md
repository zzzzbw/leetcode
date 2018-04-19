# Maximum Depth of Binary Tree

## 原题

[Maximum Depth of Binary Tree](https://leetcode.com/explore/interview/card/top-interview-questions-easy/94/trees/555/)

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its depth = 3.

## 解题

判断最大深度

### 方法1

就是很直接的递归左右子树，然后判断左右子树哪个深度更深就返回该深度

```java
	public int maxDepth(TreeNode root) {
        if (null == root) {
            return 0;
        }
        return singleDepth(root, 1) - 1;
    }

    private int singleDepth(TreeNode node, int i) {
        if (null == node) {
            return i;
        }
        int left = singleDepth(node.left, i + 1);
        int right = singleDepth(node.right, i + 1);
        return left > right ? left : right;
    }
```

