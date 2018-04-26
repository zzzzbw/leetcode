# Convert Sorted Array to Binary Search Tree

## 原题

[Convert Sorted Array to Binary Search Tree](https://leetcode.com/explore/interview/card/top-interview-questions-easy/94/trees/631/)

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of *every* node never differ by more than 1.

**Example:**

```
Given the sorted array: [-10,-3,0,5,9],

One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5
```





## 解题

把一个有序的数组编程二分查找数

### 方法1--递归

由于二分查找数的每个根节点一定大于其左节点且小于其右节点。那么我们只要每次都把数组以中间分为两个部分，那么中间数就是这个根，左边就是这个根的左子树，右边就是这个根的右子树。然后递归遍历出每一个节点

```java
	public TreeNode sortedArrayToBST(int[] nums) {
        if (nums.length == 0) {
            return null;
        }
        TreeNode root = helper(nums, 0, nums.length - 1);
        return root;
    }

    private TreeNode helper(int[] nums, int start, int end) {
        if (start > end) {
            return null;
        }
        int middle = (end + start) / 2;
        TreeNode node = new TreeNode(nums[middle]);
        node.left = helper(nums, start, middle - 1);
        node.right = helper(nums, middle + 1, end);
        return node;
    }
```

