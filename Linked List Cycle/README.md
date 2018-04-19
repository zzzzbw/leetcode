# Linked List Cycle

## 原题

[Linked List Cycle](https://leetcode.com/explore/interview/card/top-interview-questions-easy/93/linked-list/773/)

Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

## 解题

判断一个链表是否为循环链表，且不消耗额外的空间。（给的节点不一定是头结点）

### 方法1

方法就是用快慢指针。循环链表就像一个环形跑道一样。假如两个人以不同的速度跑，迟早会相遇。所以用快慢指针，假如两个指针能相遇，说明是环形

```java
	public boolean hasCycle(ListNode head) {
        if (null == head || null == head.next) {
            return false;
        }
        ListNode fast = head;
        ListNode slow = head;
        while (null != fast && null != slow) {
            slow = slow.next;
            if (null != fast.next) {
                fast = fast.next.next;
            } else {
                return false;
            }
            if (fast == slow) {
                return true;
            }
        }
        return false;
    }
```

