# Intersection of Two Linked Lists

## 原题

[Intersection of Two Linked Lists](<https://leetcode.com/explore/interview/card/top-interview-questions-medium/107/linked-list/785/>)

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

![img](https://assets.leetcode.com/uploads/2018/12/13/160_statement.png)



begin to intersect at node c1.

 

**Example 1:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_1.png)



```
Input: intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
Output: Reference of the node with value = 8
Input Explanation: The intersected node's value is 8 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,0,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
```

 

**Example 2:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_2.png)



```
Input: intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
Output: Reference of the node with value = 2
Input Explanation: The intersected node's value is 2 (note that this must not be 0 if the two lists intersect). From the head of A, it reads as [0,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
```

 

**Example 3:**

![img](https://assets.leetcode.com/uploads/2018/12/13/160_example_3.png)



```
Input: intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
Output: null
Input Explanation: From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
```

 

**Notes:**

- If the two linked lists have no intersection at all, return `null`.
- The linked lists must retain their original structure after the function returns.
- You may assume there are no cycles anywhere in the entire linked structure.
- Your code should preferably run in O(n) time and use only O(1) memory.

## 解题

题目的意思是个两个链表，判断这两个链表是否有相同(交汇)结点。

且题目表明这两个链表没有环。

题目要求O(n)的时间复杂度和O(1)的空间复杂度

### 方法1-Hash表

查找两个相同的最直接想到就是用Hash表，先遍历一个链表的结点存到Hash表里，再遍历另一个表看看有没有相同结点，如果有那么第一个相同结点就是他们的交汇处。

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    Set<ListNode> set = new HashSet<>();
    ListNode cur = headA;
    while (cur != null) {
        set.add(cur);
        cur = cur.next;
    }
    cur = headB;
    while (cur != null) {
        if (!set.add(cur)) {
            return cur;
        }
        cur = cur.next;
    }
    return null;
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

### 方法2-相同长度

首先要了解到一个概念，如果两个链表有交汇处，那么这两个链表交汇处之后是必然是重合的，所以交汇处后面长度也必然相同。那么只要先获取A和B链表的长度，然后把其中较长的那么链表的指针向后移直到和较短的链表长度的位置，此时同时移动两个链表的指针，如果结点相同，那么就是交汇处。

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode cur = headA;
    int lengthA = 0, lengthB = 0;
    while (cur != null) {
        lengthA++;
        cur = cur.next;
    }
    cur = headB;
    while (cur != null) {
        lengthB++;
        cur = cur.next;
    }
    if (lengthA > lengthB) {
        for (int i = 0; i < lengthA - lengthB; i++) {
            headA = headA.next;
        }
    } else {
        for (int i = 0; i < lengthB - lengthA; i++) {
            headB = headB.next;
        }
    }
    while (headA != null && headB != null) {
        if (headA == headB) {
            return headA;
        }
        headA = headA.next;
        headB = headB.next;
    }

    return null;
}
```

### 方法3-首尾相接

这种方法比较巧妙，同时遍历A和B链表，如果到A的尾则从B的头开始继续往后，如果到B的尾则从A的头开始继续往后。这样如果有交汇处，那么两个指针必定会走相同长度的结点(A+B-相同结点)，然后在交汇处判定为相同结点。

```java
public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
    ListNode a = headA;
    ListNode b = headB;
    while (a != b) {
        a = (a == null) ? headB : a.next;
        b = (b == null) ? headA : b.next;
    }
    return a;
}
```






