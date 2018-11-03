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
Time complexity:
- push(x) - O(1)
- pop()
    - worst case O(n)
    - best case O(1)
    - amortized O(1)
- peek()
    - worst case O(n)
    - best case O(1)
    - amortized O(1)
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

### [L144: Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)
Given a binary tree, return the preorder traversal of its nodes' values.

Example:
```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,2,3]
```

Follow up: Recursive solution is trivial, could you do it iteratively?

#### Solution
*Method 1: Recursion*

Time complexity: O(n)

Space complexity: O(logn)

```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        
        if(root == null) {
            return result;
        }
        
        result.add(root.val);
        result.addAll(preorderTraversal(root.left));
        result.addAll(preorderTraversal(root.right));
        
        return result;
    }
}
```

*Method 2: Iteration*

Time complexity: O(n)

Space Complexity: O(logn)

```
public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Deque<TreeNode> stack = new ArrayDeque<>();
        
        if(root == null) {
            return result;
        }
        
        stack.offerFirst(root);
        
        while(!stack.isEmpty()) {
            TreeNode node = stack.pollFirst();
            result.add(node.val);
            
            if(node.right != null) {
                stack.addFirst(node.right);
            }
            
            if(node.left != null) {
                stack.addFirst(node.left);
            }
        }
        
        return result;
    }
```

### [L20: Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)
Given a string containing just the characters '(', ')', '{', '}', '\[' and '\]', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:

Input: "()"
Output: true
Example 2:

Input: "()\[\]{}"
Output: true
Example 3:

Input: "(]"
Output: false
Example 4:

Input: "(\[)\]"
Output: false
Example 5:

Input: "{\[\]}"
Output: true

#### Solution

Time complexity: O(n)

Space complexity: O(n)

```
class Solution {
    public boolean isValid(String s) {
        if(s.length() == 0) {
            return true;
        }
        
        char[] chars = s.toCharArray();
        Deque<Character> stack = new ArrayDeque<>();
        Map<Character, Character> mapping = new HashMap<>();
        mapping.put(')', '(');
        mapping.put('}', '{');
        mapping.put(']', '[');
        
        for(char c: chars) {
            if(c == '(' || c == '{' || c == '[') {
                stack.offerFirst(c);
            } else {
                if(stack.pollFirst() != mapping.get(c)) {
                    return false;
                }
            }
        }
        
        return stack.isEmpty();
    }
}
```

### [L150: Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)

Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each operand may be an integer or another expression.

Note:

Division between two integers should truncate toward zero.
The given RPN expression is always valid. That means the expression would always evaluate to a result and there won't be any divide by zero operation.

Example 1:

Input: \["2", "1", "+", "3", "*"\]
Output: 9
Explanation: ((2 + 1) * 3) = 9
Example 2:

Input: \["4", "13", "5", "/", "+"\]
Output: 6
Explanation: (4 + (13 / 5)) = 6
Example 3:

Input: \["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"\]
Output: 22
Explanation: 
  ((10 * (6 / ((9 + 3) * -11))) + 17) + 5
= ((10 * (6 / (12 * -11))) + 17) + 5
= ((10 * (6 / -132)) + 17) + 5
= ((10 * 0) + 17) + 5
= (0 + 17) + 5
= 17 + 5
= 22

#### Solution

Time complexity: O(n)

Space complexity: O(n)

```
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new ArrayDeque<>();
        
        for (String token: tokens) {
            if (token.equals("+") || token.equals("-") || token.equals("*") || token.equals("/")) {
                int secondOperand = stack.pollFirst();
                int firstOperand = stack.pollFirst();
                int result = 0;
                
                switch(token) {
                    case "+":
                        result = firstOperand + secondOperand;
                        break;
                    case "-":
                        result = firstOperand - secondOperand;
                        break;
                    case "*":
                        result = firstOperand * secondOperand;
                        break;
                    case "/":
                        result = firstOperand / secondOperand;
                        break;
                }
                
                stack.offerFirst(result);
            } else {
                stack.offerFirst(Integer.parseInt(token));
            }
        }
        
        return stack.pollFirst();
    }
}
```

### [L155: Min Stack]()

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

- push(x) -- Push element x onto stack.
- pop() -- Removes the element on top of the stack.
- top() -- Get the top element.
- getMin() -- Retrieve the minimum element in the stack.

Example:

MinStack minStack = new MinStack();

minStack.push(-2);

minStack.push(0);

minStack.push(-3);

minStack.getMin();   --> Returns -3.

minStack.pop();

minStack.top();      --> Returns 0.

minStack.getMin();   --> Returns -2.

#### Solution
```
class MinStack {
    Deque<Integer> stack;
    Deque<Integer> globalMin;
    
    /** initialize your data structure here. */
    public MinStack() {
        stack = new ArrayDeque<>();
        globalMin = new ArrayDeque<>();
    }
    
    public void push(int x) {
        stack.offerFirst(x);
        if(!globalMin.isEmpty()) {
            int currentGlobalMin = globalMin.peekFirst();
            if(currentGlobalMin > x) {
                globalMin.offerFirst(x);
            } else {
                globalMin.offerFirst(currentGlobalMin);
            }
        } else {
            globalMin.offerFirst(x);
        }
    }
    
    public void pop() {
        stack.pollFirst();
        globalMin.pollFirst();
    }
    
    public int top() {
        return stack.peekFirst();
    }
    
    public int getMin() {
        return globalMin.peekFirst();
    }
}
```

[L621: Task Scheduler](https://leetcode.com/problems/task-scheduler/)

Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks.Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.

However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.

You need to return the least number of intervals the CPU will take to finish all the given tasks.

Example:

Input: tasks = \["A","A","A","B","B","B"\], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.

Note:

The number of tasks is in the range [1, 10000].
The integer n is in the range [0, 100].

```
class Solution {
    public int leastInterval(char[] tasks, int n) {
        if(n <= 0) {
            return tasks.length;
        }
        
        int[] taskCount = new int[26];
        
        for(char task: tasks) {
            taskCount[task - 'A']++;
        }
        
        Arrays.sort(taskCount);
        int time = 0;
        
        while(taskCount[25] > 0) {
            for(int i = 0; i <= n; i++) {
                if(taskCount[25] == 0) {
                    break;
                }
                
                if(i < 26 && taskCount[25 - i] > 0) {
                    taskCount[25 - i]--;
                }
                
                time++;
            }
            
            Arrays.sort(taskCount);
        }
        
        return time;
    }
}
```

[L456: 132 Pattern](https://leetcode.com/problems/132-pattern/)

Given a sequence of n integers a1, a2, ..., an, a 132 pattern is a subsequence ai, aj, ak such that i < j < k and ai < ak < aj. Design an algorithm that takes a list of n numbers as input and checks whether there is a 132 pattern in the list.

Note: n will be less than 15,000.


Example 1:

Input: \[1, 2, 3, 4\]

Output: False

Explanation: There is no 132 pattern in the sequence.


Example 2:

Input: \[3, 1, 4, 2\]

Output: True

Explanation: There is a 132 pattern in the sequence: \[1, 4, 2\].


Example 3:

Input: \[-1, 3, 2, 0\]

Output: True

Explanation: There are three 132 patterns in the sequence: \[-1, 3, 2\], \[-1, 3, 0\] and \[-1, 2, 0\].

```
class Solution {
    public boolean find132pattern(int[] nums) {
        if(nums.length == 0) {
            return false;
        }
        
        int min = Integer.MAX_VALUE;
        
        for (int j = 0; j < nums.length - 1; j++) {
            min = nums[j] < min ? nums[j] : min;
            for (int k = j + 1; k < nums.length; k++) {
                if (nums[k] > min && nums[j] > nums[k])
                    return true;
            }
        }
        return false;
    }
}
```
