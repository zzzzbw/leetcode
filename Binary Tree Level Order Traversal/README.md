# Binary Tree Level Order Traversal

## 原题

[Binary Tree Level Order Traversal](https://leetcode.com/explore/interview/card/top-interview-questions-easy/94/trees/628/)

Given a binary tree, return the *level order* traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```



## 解题

把树的每层都变为一个数组返回

### 方法1--递归

通过递归，类似于后序遍历的方法，设置每一层的List

```java
	public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> container = new ArrayList<>();
        if (null == root) {
            return container;
        }
        order(root, 0, container);
        return container;
    }

    private void order(TreeNode node, int level, List<List<Integer>> container) {
        if (null == node) {
            return;
        }
        if (level > container.size() - 1) {
            container.add(new ArrayList<>());
        }
        order(node.left, level + 1, container);
        order(node.right, level + 1, container);
        List<Integer> list = container.get(level);
        list.add(node.val);
        container.set(level, list);
    }
```

