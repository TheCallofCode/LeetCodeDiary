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


#### Solution

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

### [L232: Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/)
Implement the following operations of a queue using stacks.

push(x) -- Push element x to the back of queue.
pop() -- Removes the element from in front of queue.
peek() -- Get the front element.
empty() -- Return whether the queue is empty.

Example:
```
MyQueue queue = new MyQueue();

queue.push(1);
queue.push(2);  
queue.peek();  // returns 1
queue.pop();   // returns 1
queue.empty(); // returns false
```

Notes:

- You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
- Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
- You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

#### Solution

```
class MyQueue {
    Deque<Integer> storeStack;
    Deque<Integer> popStack;
    /** Initialize your data structure here. */
    public MyQueue() {
        storeStack = new ArrayDeque<>();
        popStack = new ArrayDeque<>();
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        storeStack.offerFirst(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if(popStack.isEmpty()) {
            feedPopStack();
        }
        
        return popStack.pollFirst();
    }
    
    /** Get the front element. */
    public int peek() {
        if(popStack.isEmpty()) {
            feedPopStack();
        }
        
        return popStack.peekFirst();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return storeStack.isEmpty() && popStack.isEmpty();
    }
    
    // move all items in storeStack to popStack
    private void feedPopStack() {
        while(storeStack.size() > 0) {
            popStack.offerFirst(storeStack.pollFirst());
        }
    }
}
```
