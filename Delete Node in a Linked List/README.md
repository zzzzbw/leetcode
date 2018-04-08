# Delete Node in a Linked List

## 原题

[Delete Node in a Linked List](https://leetcode.com/explore/interview/card/top-interview-questions-easy/93/linked-list/553/)

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is `1 -> 2 -> 3 -> 4` and you are given the third node with value `3`, the linked list should become `1 -> 2 -> 4` after calling your function.

## 解题

这题主要是理解一下题目的意思。就是指删除一个链表中的一个节点。但是给的方法是要被删除的节点的对象。

### 方法1

由于给的是要被删除的节点，所以就获取不到这个节点的上一个节点。不过只要将这个节点的下一个节点覆盖这个节点，就相当于删除了这个节点。另外由于题目说被删除的节点不是最后一个，所以不用考虑下一个节点为null的情况

```java
   /**
     * Definition for singly-linked list.
     * public class ListNode {
     *     int val;
     *     ListNode next;
     *     ListNode(int x) { val = x; }
     * }
     */
	public void deleteNode(ListNode node) {
        if (node == null) {
            return;
        }
        node.val = node.next.val;
        node.next = node.next.next;
    }
```
