# Linked List Practices

### [L2: Add Two Numbers](https://leetcode.com/problems/add-two-numbers/)
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.

My Solution:
```
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        if(l1 == null) {
            return l1;
        }
        
        if(l2 == null) {
            return l2;
        }
        
        ListNode dummy = new ListNode(0);
        ListNode cur = dummy;
        int carry = 0;
        int sum = 0;
        
        while(l1 != null || l2 != null) {
            if(l1 != null && l2 != null) {
                sum = l1.val + l2.val + carry;    
            } else if(l1 != null) {
                sum = l1.val + carry;
            } else if(l2 != null) {
                sum = l2.val + carry;
            }
            
            int curValue = sum % 10;
            carry = sum / 10;
            
            ListNode node = new ListNode(curValue);
            cur.next = node;
            cur = cur.next;
            
            if(l1 != null) {
                l1 = l1.next;    
            }
            
            if(l2 != null) {
                l2 = l2.next;
            }
        }
        
        if(l1 == null && l2 == null && carry > 0) {
            ListNode node = new ListNode(carry);
            cur.next = node;
        }
        
        return dummy.next;
    }
}
```

### [L24: Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/)
Given a linked list, swap every two adjacent nodes and return its head.

Example:

Given 1->2->3->4, you should return the list as 2->1->4->3.
Note:

Your algorithm should use only constant extra space.
You may not modify the values in the list's nodes, only nodes itself may be changed.

```
class Solution {
    public ListNode swapPairs(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode cur = head;
        
        while(prev.next != null && prev.next.next != null) {
            prev.next = prev.next.next;
            ListNode nextPair = prev.next.next;
            prev.next.next = cur;
            cur.next = nextPair;
            prev = cur;
            cur = cur.next;
        }
        
        return dummy.next;
    }
}
```

### [L25: Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)
Given a linked list, reverse the nodes of a linked list k at a time and return its modified list.

k is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

Example:

Given this linked list: 1->2->3->4->5

For k = 2, you should return: 2->1->4->3->5

For k = 3, you should return: 3->2->1->4->5

Note:

- Only constant extra memory is allowed.
- You may not alter the values in the list's nodes, only nodes itself may be changed.
```
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        if(head == null || head.next == null || k <= 1) {
            return head;
        }
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        while(head.next != null) {
            head = reverseKNodes(head, k);
        }
        
        return dummy.next;
    }
    
    private ListNode reverseKNodes(ListNode tailOfPrevKNodes, int k) {
        ListNode node = tailOfPrevKNodes;
        
        for(int i = 0; i < k; i++) {
            if(node.next == null) {
                return node;
            }
            
            node = node.next;
        }
        
        ListNode prev = tailOfPrevKNodes;
        ListNode cur = tailOfPrevKNodes.next;
        ListNode tailOfCurKNodes = tailOfPrevKNodes.next;
        
        for(int i = 0; i < k; i++) {
            ListNode temp = cur.next;
            cur.next = prev;
            prev = cur;
            cur = temp;
        }
        
        tailOfPrevKNodes.next = prev;
        tailOfCurKNodes.next = cur;
        
        return tailOfCurKNodes;
    }
}
```

### [L138: Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer)

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

```
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null) {
            return head;
        }
        
        Map<RandomListNode, RandomListNode> mapping = new HashMap<>();
        
        RandomListNode node = head;
        RandomListNode dummy = new RandomListNode(0);
        RandomListNode copyNode = dummy;
        
        //copy all nodes and create mapping
        while(node != null) {
            RandomListNode copy = new RandomListNode(node.label);
            mapping.put(node, copy);
            copyNode.next = copy;
            copyNode = copyNode.next;
            node = node.next;
        }
        
        //copy all random nodes
        node = head;
        copyNode = dummy.next;
        while(node != null) {
            copyNode.random = mapping.get(node.random);
            copyNode = copyNode.next;
            node = node.next;
        }
        
        return dummy.next;
    }
}
```

### [L206: Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/)
Reverse a singly linked list.

Example:

Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL

Follow up:

A linked list can be reversed either iteratively or recursively. Could you implement both?

```
class Solution {
    //Iteration
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        
        ListNode prev = null;
        
        while(head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        
        return prev;
    }
    
    //Recursion
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        
        ListNode next = head.next;
        
        ListNode newHead = reverseList(head.next);
        
        next.next = head;
        head.next = null;
        
        return newHead;
    }
}
```

### [L143: Reorder List](https://leetcode.com/problems/reorder-list/)
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

*Example 1:*

Given 1->2->3->4, reorder it to 1->4->2->3.

*Example 2:*

Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

```
class Solution {
    public void reorderList(ListNode head) {
        if(head == null || head.next == null || head.next.next == null) {
            return;
        }
        
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        ListNode headOfSecondHalf = reverseList(slow.next);
        
        slow.next = null;
        
        ListNode curOfFirstHalf = head;
        ListNode curOfSecondHalf = headOfSecondHalf;
        while(curOfSecondHalf != null) {
            ListNode tempOfFirst = curOfFirstHalf.next;
            ListNode tempOfSecond = curOfSecondHalf.next;
            curOfFirstHalf.next = curOfSecondHalf;
            curOfSecondHalf.next = tempOfFirst;
            curOfFirstHalf = tempOfFirst;
            curOfSecondHalf = tempOfSecond;
        }
        
        return;
    }
    
    private ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        
        ListNode prev = null;
        
        while(head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        
        return prev;
    }
}
```

### [L234: Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

Given a singly linked list, determine if it is a palindrome.

Example 1:

Input: 1->2
Output: false
Example 2:

Input: 1->2->2->1
Output: true

Follow up:
Could you do it in O(n) time and O(1) space?

```
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head == null || head.next == null) {
            return true;
        }
        
        ListNode slow = head;
        ListNode fast = head;
        
        while(fast.next != null && fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        
        ListNode headOf2ndHalf = reverseList(slow.next);
        ListNode curOf2ndHalf = headOf2ndHalf;
        ListNode curOf1stHalf = head;
        while(curOf2ndHalf != null) {
            if(curOf2ndHalf.val != curOf1stHalf.val) {
                return false;
            }
            curOf2ndHalf = curOf2ndHalf.next;
            curOf1stHalf = curOf1stHalf.next;
        }
        
        return true;
    }
    
    private ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        
        ListNode prev = null;
        
        while(head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
}
```
