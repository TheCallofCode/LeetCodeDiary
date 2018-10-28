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

### [L24: Swap Nodes in Pairs] (https://leetcode.com/problems/swap-nodes-in-pairs/)
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
