# Palindrome Linked List

## 原题

[Palindrome Linked List](https://leetcode.com/explore/interview/card/top-interview-questions-easy/93/linked-list/772/)

Given a singly linked list, determine if it is a palindrome.

**Follow up:**
Could you do it in O(n) time and O(1) space?

## 解题

判断一个链表是否为回文链表，且要求时间复杂度为O(n)，空间复杂度为O(1)

### 方法1

判断回文最关键的是要找到中间位置，然后才可以开始比较前后是否一致。链表找到中间位置的方法就是用快慢指针。快指针每次向前两个节点，慢指针每次向前一个节点，等到快指针指向最后的时候，慢指针指的就是中间节点。

然后就是判断前面和后面是否一样了。这里用的是栈的方法，在找中间节点的时候把前面一半放到栈中，然后迭代后面一半的时候利用栈的先进后出原理比对是否一样。

只是这种方法空间复杂度不是O(1)

```java
	public boolean isPalindrome(ListNode head) {
        if (null == head || null == head.next) {
            return true;
        }
        Stack<Integer> stack = new Stack<>();
        ListNode slow = head;
        ListNode fast = head;
        while (null != fast && null != fast.next) {
            // 放到栈中
            stack.push(slow.val);
            slow = slow.next;
            fast = fast.next.next;
        }
        // 链表奇数个时，此时慢指针指着中间节点，向前移动一步
        if (null != fast) {
            slow = slow.next;
        }
        while (null != slow) {
            // 先进后出原理，比较是否一样
            if (!stack.pop().equals(slow.val)) {
                return false;
            }
            slow = slow.next;
        }
        return true;
    }
```

### 方法2

原理和方法1一样，只是不用栈来比对了，而是在找到中间节点之后，把后面一半翻转，这时候比对和前面一半是否一样就可以了。这种方法时间复杂度为O(n)，空间复杂度为O(1)

```java
     public boolean isPalindrome(ListNode head) {
        if (null == head || null == head.next) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (null != fast && null != fast.next) {
            slow = slow.next;
            fast = fast.next.next;
        }
        // 链表奇数个时，此时慢指针指着中间节点，向前移动一步
        if (null != fast) {
            slow = slow.next;
        }

        //翻转链表 
        ListNode halfHead = slow;
        ListNode node = slow.next;
        while (null != node) {
            ListNode tmp = node.next;
            node.next = halfHead;
            halfHead = node;
            node = tmp;
        }
        slow.next = null;
        showList(halfHead);
        while (null != halfHead) {
            if (halfHead.val != head.val) {
                return false;
            }
            halfHead = halfHead.next;
            head = head.next;
        }
        return true;
    }
```

