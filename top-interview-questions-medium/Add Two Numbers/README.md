# Add Two Numbers

## 原题

[Add Two Numbers](<https://leetcode.com/explore/interview/card/top-interview-questions-medium/107/linked-list/783/>)

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

## 解题

题目意思是把两个链表的按照数字的形式相加，并以链表的形式返回结果

### 方法1

这题其实很简单，因为链表是从最小位数(个位数)开始遍历的，所以只要同时遍历两个链表然后对应位数相加。注意点：1. 注意两个链表不一定长度相同，所以每次遍历都要判断结点是否为null，为null的话则该值为0 2.注意保存进位 3. 遍历结束之注意后还要再判断是否有进位

```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode head = new ListNode(-1);
    ListNode cur = head;
    int carry = 0;
    while (l1 != null || l2 != null) {
        int num1 = l1 == null ? 0 : l1.val;
        int num2 = l2 == null ? 0 : l2.val;
        int num = num1 + num2 + carry;
        carry = num >= 10 ? 1 : 0;
        cur.next = new ListNode(num % 10);
        cur = cur.next;
        if (l1 != null) {
            l1 = l1.next;
        }
        if (l2 != null) {
            l2 = l2.next;
        }
    }
    if (carry == 1) {
        cur.next = new ListNode(1);
    }
    return head.next;
}
```



