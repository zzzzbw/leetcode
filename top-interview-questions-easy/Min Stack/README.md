# Min Stack 

## 原题

[Min Stack ](https://leetcode.com/explore/interview/card/top-interview-questions-easy/98/design/562/)

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

## 解题

题目要求就是实现一个栈，主要除了`pop()`和`push()`等方法外，还有`getMin()`方法，这个方法要返回栈中最小的值。

### 方法1

主要就是要实现`getMin()`方法，在这里是把栈当做单链表来遍历所有值，得到最小值。这个方法时间复杂度高。

```java
class MinStack {
	private StackItem top;
    
	public MinStack() {
	}

	public void push(int x) {
		StackItem add = new StackItem();
		add.num = x;
		add.next = this.top;
		this.top = add;
	}

	public void pop() {
		if (top != null) {
			top = top.next;
		}
	}

	public int top() {
		return top.num;
	}

	public int getMin() {
		if (null == top) {
			return 0;
		}
		int min = top.num;
		StackItem item = top.next;
		while (item != null) {
			if (min > item.num) {
				min = item.num;
			}
			item = item.next;
		}
		return min;
	}

	private class StackItem {
		int num;
		StackItem next;
	}
}
```

### 方法2 

这个方法是除了一个存储顺序push进来的栈，还要一个存储一个出现过的最小值的栈。当push进来时，比较当前值和`minStack`栈顶值大小，如果小于栈顶值，则push进`minStack`。当pop时，如果`top`栈顶值和`minStack`栈顶值相同，说明当前最小值被pop出去了，就也把`minStack`栈顶pop出去。

```java
class MinStack {
	private StackItem top;
	private StackItem minStack;

	public MinStack() {
	}

	public void push(int x) {
		StackItem add = new StackItem();
		add.num = x;
		add.next = this.top;
		this.top = add;
		if (minStack == null || minStack.num >= x) {
			StackItem min = new StackItem();
			min.num = x;
			min.next = this.minStack;
			this.minStack = min;
		}
	}

	public void pop() {
		if (top != null) {
			if (minStack != null && top.num == minStack.num) {
				minStack = minStack.next;
			}
			top = top.next;
		}
	}

	public int top() {
		return top.num;
	}

	public int getMin() {
		if (null == minStack) {
			return 0;
		}
		return minStack.num;
	}

	private class StackItem {
		int num;
		StackItem next;
	}
}
```



