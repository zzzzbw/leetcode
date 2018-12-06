# Symmetric Tree

## 原题

[Symmetric Tree](https://leetcode.com/explore/interview/card/top-interview-questions-easy/94/trees/627/)

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3
```

**Note:**
Bonus points if you could solve it both recursively and iteratively.



## 解题

判断一个树是否对称

### 方法1--递归

通过递归直接判断对称位置的节点是否相同

```java
	// 递归方法
    public boolean isSymmetric(TreeNode root) {
        if (null == root) {
            return true;
        }
        return compare(root.left, root.right);
    }

    private boolean compare(TreeNode left, TreeNode right) {
        if (null == left && null == right) {
            return true;
        }
        if (null == left || null == right) {
            return false;
        }
        if (left.val != right.val) {
            return false;
        }
        return compare(left.left, right.right) && compare(left.right, right.left);
    }
```

### 方法2--迭代

迭代一个二叉树主要是要利用栈，就和图的深度遍历一样，通过栈来遍历。

然后是两个要判断的节点的左右子树为空的情况是否一样。

```java
	public boolean isSymmetric1(TreeNode root) {
        if (null == root) {
            return true;
        }
        if ((null == root.left && null != root.right)
                || (null != root.left && null == root.right)) {
            return false;
        }
        if (null == root.left && null == root.right) {
            return true;
        }

        Stack<TreeNode> s1 = new Stack<>();
        Stack<TreeNode> s2 = new Stack<>();
        s1.push(root.left);
        s2.push(root.right);
        while (!s1.isEmpty() && !s2.isEmpty()) {
            TreeNode n1 = s1.pop();
            TreeNode n2 = s2.pop();

            if (n1.val != n2.val) {
                return false;
            }
            boolean flag =
                    (n1.left == null && n2.right != null) || (n1.right == null && n2.left != null)
                            || (n1.left != null && n2.right == null)
                            || (n1.right != null && n2.left == null);
            if (flag) {
                return false;
            }

            if (n1.left != null && n2.right != null) {
                s1.push(n1.left);
                s2.push(n2.right);
            }
            if (n1.right != null && n2.left != null) {
                s1.push(n1.right);
                s2.push(n2.left);
            }
        }

        return true;
    }
```

