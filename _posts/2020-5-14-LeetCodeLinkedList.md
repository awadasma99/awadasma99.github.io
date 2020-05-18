---
layout: post
title: Working Through Some Linked List LeetCode Problems 
---

In one of my previous posts, titled "Interview Prep," I mentioned that I had run through a number of LeetCode problems of various kinds in preparation for an interview. In this post, I plan to go through some Linked List problems, noting the steps I took along the way. 

## Problem 1 

*Reverse a singly Linked List* 
    
    Definition of a singly-linked list:
    
    public class ListNode {
      int val;
      ListNode next;
      ListNode(int x) { val = x; }
    }
    
    Example: 
    
    Input: 1->2->3->4->5->NULL
    Output: 5->4->3->2->1->NULL

*A linked list can be reversed either iteratively or recursively. Could you implement both?* 

When I approach LinkedList problems, I find that using a pointer tends to be a good method to have in mind. I imagine that a brute force algorithm could look something like copying the elements of this list to the end of a new list, but the problem itself makes no mention of methods such as addLast, so I feel that they are looking to test direct manipulation of the list given. 

Iteratively, I think that the way to go about this involves something that would look like repeated swaps throughout the list. Ultimately, what you're doing is swapping the references from forwards to backwards. Given that we don't have access to a previous, as we would with a doubly linked list, this is where a pointer comes in. 

We'd first want to make it so that the beginning of the given list points to NULL, as seen in the provided example. That hints that we can initialize our pointer, or one of them, to null. At this point, then, as we iterate through the list, we want to swap the reference of the current node with the reference of the one before it. So, instead of having 2 point to 3, we want 3 to point to 2. 

At the end, we return the head of our newly reversed linked list. 

This would look something like this, with an O(n) solution, n being the size of the list: 
        
        public ListNode reverseList(ListNode head) {
            ListNode newH = null;
        
            while (head != null) {
                ListNode next = head.next;
                head.next = newH;
                newH = head;
                head = next;
            }
            return newH;
        }

Recursively, it's a little trickier to think about, but if we use head recursion, we can get to the second to last node of the LinkedList by simply calling the method with the head's next as the parameter until we find the head or the head's next to be null. Then we change the references. We'd want the reference of the next node to be equal to the current node— in other words, head.next.next = head. This would look something like this: 

        public ListNode reverseList(ListNode head) {
            if (head == null || head.next == null) 
                return head;
            ListNode p = reverseList(head.next);
            head.next.next = head;
            head.next = null;
            return p;
        }

The time complexity's pretty much the same here, O(n), but the space complexity is definitely worse off, considering the space in memory taken for remembering each recursive call assignment— I believe it would be at O(n), where n is the size of the list. 

----

## Problem 2 

*Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.*
    
    Example: 
        Input: head = [4,5,1,9], node = 5
        Output: [4,1,9]
        Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function. 

In this problem, the definition of a singly-linked list is the same as that in the previous problem. We only have access to each the node to be deleted, the node's next, and the data of each node we have access to. With this given information in mind, what we can do is make it seem like we deleted the node. 

By that, I mean that we copy the data of the next node into the node reference we are given (so [4, 5, 1, 9], would look like [4, 1, 1, 9] instead) and then delete that next node by changing some references. Essentially, we made it look like we deleted the node reference provided, but really we deleted its data from the list. 

We'd change the references such that the node's next is equal to it's initial next's next. So, the second node would point to the third node's next, the fourth node, instead of the third node, for instance. In effect, [4, 1, 1, 9] becomes [4, 1, 9], as expected. 

The code for this is pretty simple: 

        public void deleteNode(ListNode node) {
            node.val = node.next.val; 
            node.next = node.next.next; 
        }
 
Runtime and space complexity would be O(1), since we're merely copying data and changing a single reference, using no extra space, and doing only these set of actions regardless of the input size. 
