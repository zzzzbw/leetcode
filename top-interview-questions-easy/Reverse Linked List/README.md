# Reverse Linked List

## 原题

[Reverse Linked List](https://leetcode.com/explore/interview/card/top-interview-questions-easy/93/linked-list/560/)

Reverse a singly linked list.

Hint:

A linked list can be reversed either iteratively or recursively. Could you implement both?

## 解题

题目意思让你翻转一个链表，可以用迭代或者递归的方式做。暂时只想到迭代的

### 方法1

设置一个新的头结点，然后迭代原来的链表，把每个结点都插入到这个心的头结点和下一个头结点之间。

原链表:1--> 2 --> 3 --> 4

新: newHead -- > 1

​	newHead --> 2 -- > 1

​	newHead --> 3 --> 2 --> 1

​	newHead -- > 4 --> 3 --> 2 -- > 1



```java
	public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = new ListNode(0);
        ListNode node = head;
        while (null != node) {
            ListNode temp = newHead.next;
            ListNode next = new ListNode(node.val);
            next.next = temp;
            newHead.next = next;
            node = node.next;
        }

        return newHead.next;
    }
```

### 方法2

和方法1的意思是一样的，只是方法一其实在倒转的过程中有`new ListNode(node.val)`，会占用空间。方法2在迭代的时候用`ListNode tmp = node.next;`来保存下一个要迭代的节点。

```java
	public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = head;
        ListNode node = newHead.next;
        while (null != node) {
            ListNode tmp = node.next;
            node.next = newHead;
            newHead = node;
            node = tmp;
        }
        head.next = null;
        return newHead;
    }
```

