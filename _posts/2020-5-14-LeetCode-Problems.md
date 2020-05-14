---
layout: post
title: Working Through Some LeetCode Problems 
---

In one of my previous posts, titled "Interview Prep," I mentioned that I had gone through a number of LeetCode problems in preparation for a technical interview. In this post, I'll go through a few of them, noting the steps I took and what I learned from them. 

## Problem 1 

Given a binary tree, return the inorder traversal of its nodes' values.

    Input: [1, null, 2, 3] 
    
      1
       \
        2
       /
      3 
      
    Output: [1, 3, 2] 

So, from my understanding, an inorder traversal follows a Left-Node-Right track, meaning that you would traverse the left branch of a given tree until you hit null, then return the root, then traverse the right branch of the tree. In the example, since 1 has no left branch, you return 1, then traverse its right. The left of 2 is then traversed, returning 3, followed by the root, 2. There is no right branch, so you've traversed the tree. 

