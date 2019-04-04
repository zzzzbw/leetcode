# Odd Even Linked List

## 原题

[Odd Even Linked List](<https://leetcode.com/explore/interview/card/top-interview-questions-medium/107/linked-list/784/>)

Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

**Example 1:**

```
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL
```

**Example 2:**

```
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
```

**Note:**

- The relative order inside both the even and odd groups should remain as it was in the input.
- The first node is considered odd, the second node even and so on ...

## 解题

题目意思是把一个链表的奇数位结点放在前面，偶数位结点放在后面。注意是结点的位置而不是结点的值。另外要求空间复杂度O(1)时间复杂度O(n)

### 方法1

这题用两个头结点分别存储奇数位结点和偶数位结点(因为只用new一个ListNode头节点而其他结点都是原有的，所以符合空间复杂度要求)，然后遍历链表把结点对应保存。注意点：1. 遍历结束后要把偶数结点的最后结点next置为null，否则由于`odd.next = evenHead.next;`链接两个结点的时候有可能形成环。

```java
public ListNode oddEvenList(ListNode head) {
    int index = 0;
    ListNode oddHead = new ListNode(-1);
    ListNode odd = oddHead;
    ListNode evenHead = new ListNode(-1);
    ListNode even = evenHead;
    ListNode cur = head;
    while (cur != null) {
        index++;

        if (index % 2 == 0) {
            even.next = cur;
            even = even.next;
        } else {
            odd.next = cur;
            odd = odd.next;
        }
        cur = cur.next;
    }
    even.next = null;

    odd.next = evenHead.next;
    return oddHead.next;
}
```



