---
layout: post
title: Working Through Some LeetCode Problems 
---

In one of my previous posts, titled "Interview Prep," I mentioned that I had gone through a number of LeetCode problems in preparation for a technical interview. In this post, I'll go through a few of them, noting the steps as I go along. 

## Problem 1 

Given the following TreeNode class: 

    public class TreeNode {
        int val;
        TreeNode left;
        TreeNode right;
        TreeNode(int x) { val = x; }
    }
    
Given a binary tree, return the inorder traversal of its nodes' values.

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


## Problem 2 

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

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
