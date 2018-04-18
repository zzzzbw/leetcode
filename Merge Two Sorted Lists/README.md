# Merge Two Sorted Lists

## 原题

[Merge Two Sorted Lists](https://leetcode.com/explore/interview/card/top-interview-questions-easy/93/linked-list/771/)

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```

## 解题

题目意思就是连接两个有序的链表。

### 方法1

就是两个指针分别指向两个链表，当某个节点值小的时候就插入到新链表中，然后该链表指针向前移动。需要注意的是当遍历完一个链表后，记得把另一个链表剩下的值插入到结果链表后。

```java
	public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode newHead = new ListNode(-1);
        ListNode cur = newHead;
        while (null != l1 && null != l2) {
            if (l1.val < l2.val) {
                cur.next = l1;
                l1 = l1.next;
            } else {
                cur.next = l2;
                l2 = l2.next;
            }
            cur = cur.next;
        }
        if (null == l1) {
            cur.next = l2;
        }
        if (null == l2) {
            cur.next = l1;
        }
        return newHead.next;
    }
```
