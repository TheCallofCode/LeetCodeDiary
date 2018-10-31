### [L225: Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)
Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.

Example:
```
MyStack stack = new MyStack();

stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false
```
Notes:

- You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
- Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
- You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

*Method 1*

Using 2 queues.
Time complexity:
- push(x) - O(1)
- pop() - O(n)
- top() - O(1)

```
class MyStack {
    private Queue<Integer> container;
    private Queue<Integer> tempContainer;
    private int top;
    /** Initialize your data structure here. */
    public MyStack() {
        container = new LinkedList<>();
        tempContainer = new LinkedList<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        container.offer(x);
        top = x;
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        while(container.size() > 1) {
            top = container.poll();
            tempContainer.offer(top);
        }
        
        int topVal = container.poll();
        Queue<Integer> temp = container;
        container = tempContainer;
        tempContainer = temp;
        
        return topVal;
    }
    
    /** Get the top element. */
    public int top() {
        return top;
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return container.isEmpty();
    }
}
```

*Method 2*

Using 1 queue.
Time complexity:
- push(x) - O(n)
- pop() - O(1)
- top() - O(1)

```
class MyStack {
    private Queue<Integer> container;
    private int top;
    /** Initialize your data structure here. */
    public MyStack() {
        container = new LinkedList<>();
    }
    
    /** Push element x onto stack. */
    public void push(int x) {
        int sizeBeforePush = container.size();
        container.offer(x);
        while(sizeBeforePush > 0) {
            container.offer(container.poll());
            sizeBeforePush--;
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    public int pop() {
        return container.poll();
    }
    
    /** Get the top element. */
    public int top() {
        return container.peek();
    }
    
    /** Returns whether the stack is empty. */
    public boolean empty() {
        return container.isEmpty();
    }
}
```
