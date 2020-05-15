---
layout: post
title: Working Through Some Binary Tree LeetCode Problems 
---

In one of my previous posts, titled "Interview Prep," I mentioned that I had gone through a number of LeetCode problems in preparation for a technical interview. In this post, I'll go through a few of them, particularly binary tree problems, noting the steps as I go along. 

## Problem 1 

*Given the following TreeNode class:* 

    public class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }
    
*Given a binary tree, return the inorder traversal of its nodes' values.*

    Input: [1, null, 2, 3] 
    
      1
       \
        2
       /
      3 
      
    Output: [1, 3, 2] 

So, from my understanding, an inorder traversal follows a Left-Node-Right track, meaning that you would traverse the left branch of a given tree until you hit null, then return the root, then traverse the right branch of the tree. 
In the example, since 1 has no left branch, you return 1, then traverse its right. The left of 2 is then traversed, returning 3, followed by the root, 2. There is no right branch, so you've traversed the tree. 

When it comes to programming this, it makes sense to use a recursive approach. If you see a tree as a tree composed of other, smaller trees, then recursion, which ultimately means following the same pattern of instructions until a base case is hit, could easily be used.  

As described above, we stop traversing a branch when we hit a null branch. A null branch is simply a branch with a null root. We only want to traverse branches that aren't null. With this in mind, we can create our base case: 

        if (root != null) 
        
If the root isn't null, we then want to traverse its left, return the root node, and traverse its right. We can express this as follows: 

        if (root != null) {
            if (root.left != null)
                inOrderTraversal(root.left, list);
            
            list.add(root.val); 
            
            if (root.right != null) 
                inOrderTraversal(root.right, list); 
        }

What we're doing is essentially traversing the left until we hit null, then returning the root, then traversing the right until we hit null for each subtree of the tree given.

Runtime: 0 ms 

Space: 37.3 MB

----- 

## Problem 2 

*Given a binary tree, find its maximum depth.*

*The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.*

        Input: [3, 9, 20, null, null, 15, 7] 
        
                3
               / \
              9   20
                 /  \
                15   7
            
        Output: 3 

Another problem where recursion would make sense. Really what you're doing here or want to be doing is looking to find the longest path until you hit null from the root. You're comparing the length of the longest line of subtrees between the left and right of the given root. 

Our base case is, therefore, similar to that of the last, because you stop traversing, therefore adding to the length, when you hit null: 

        if (root == null)


The rest of the code would simply be what we noted above, a comparison between the left and right subtrees' lengths: 

        if (root == null)
            return 0;
        else
            return Math.max(1 + maxDepth(root.left), 1 + maxDepth(root.right));
            

Runtime: 0 ms

Space: 39.9 MB 

----- 

## Problem 3 

*Given an array where elements are sorted in ascending order, convert it to a height balanced BST.*

*For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.* 

        Given the sorted array: [-10,-3,0,5,9],

        One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

                    0
                   / \
                 -3   9
                /   /
              -10  5
              
It seems that recursion is a running method when it comes to binary tree problems. In this case, we're given an array of numbers, sorted, and are asked to distribute them in a way where each subtree's length is equal to or greater than/less than the depth of another by only one. 

This one had me thinking for a while, but the word sorted got me thinking of a binary search. In a binary search, we repeatedly halve the input until we find a certain value. Here, we can use that thinking in a way where we halve the input, repeatedly putting each half into the left/right of a binary tree. This way, the depths between subtrees will never differ by more than one. 

I created a helper method, which I used to pass the "start" and "end" points so that I could shrink the input when recursively calling the method. Just as with a binary search, the base case would be when the start field is greater than the end. 

        public TreeNode sortedArrayToBSTHelper(int[] nums, int start, int end) {
            if (start > end)
                return null;
        
            int mid = (start + end) / 2;
        
            TreeNode n = new TreeNode(nums[mid]);
            n.left = sortedArrayToBSTHelper(nums, start, mid-1);
            n.right = sortedArrayToBSTHelper(nums, mid+1, end);
        
            return n; 
        }
        
Here, I create a TreeNode, assign the lower half of the input to the left of the node, the higher half to the node, and the data of the middle value to the node itself.

The output would look as follows:

        [0,-10,5,null,-3,null,9]
        
                0 
               / \
             -10  5
                \  \
                 -3 9
        
        a height-balanced binary tree 
        
Runtime: 0 ms

Space: 39.3 MB 
                     
                      
