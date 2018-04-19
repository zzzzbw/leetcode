# Validate Binary Search Tree

## 原题

[Validate Binary Search Tree](https://leetcode.com/explore/interview/card/top-interview-questions-easy/94/trees/625/)

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Example 1:**

```
Input:
    2
   / \
  1   3
Output: true
```

**Example 2:**

```
    5
   / \
  1   4
     / \
    3   6
Output: false
Explanation: The input is: [5,1,4,null,null,3,6]. The root node's value
             is 5 but its right child's value is 4.
```

## 解题

判断一个树是否为搜索二叉树

定义：左<根<右，且一个节点左边左右元素都小于他，右边所有元素都大于他

### 方法1

由于一个搜索二叉树中序遍历之后是一个有序数组，所以只用先中序遍历，然后判断数组是否为有序

```java
	// 中序遍历法
    public boolean isValidBST(TreeNode root) {
        if (root == null) {
            return true;
        }
        List<Integer> list = new ArrayList<>();
        middle(root, list);
        for (int i = 0; i < list.size() - 1; i++) {
            if (list.get(i) >= list.get(i + 1)) {
                return false;
            }
        }
        return true;
    }

    private void middle(TreeNode node, List<Integer> list) {
        if (null == node) {
            return;
        }
        middle(node.left, list);
        list.add(node.val);
        middle(node.right, list);
    }
```

### 方法2

用递归的方式验证左子树小于其所有父节点，右子树大于其所有父节点。注意初始值用Long，因为有可能有int边界。

```java
	public boolean isValidBST(TreeNode root) {
        return valid(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    private boolean valid(TreeNode node, long low, long high) {
        if (node == null) {
            return true;
        }
        if (low >= node.val || high <= node.val) {
            return false;
        }
        if (null != node.left) {
            if (node.left.val >= node.val) {
                return false;
            }
        }
        if (null != node.right) {
            if (node.right.val <= node.val) {
                return false;
            }
        }
        return valid(node.left, low, node.val) && valid(node.right, node.val, high);
    }
```

