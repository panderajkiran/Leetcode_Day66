# Leetcode_Day66

# Day 66 – Binary Tree Level Order Traversal

**LeetCode Problem:** 102. Binary Tree Level Order Traversal  
**Difficulty:** Medium  
**Language:** Java  
**Status:** Accepted ✅

## Problem Description

Given the root of a binary tree, return the values of its nodes in **level order**.

Level order means visiting the tree **level by level**, from left to right.

For example:

```text
        3
       / \
      9   20
         /  \
        15   7

The level order traversal is:
[[3], [9, 20], [15, 7]]

Approach
I used Breadth-First Search (BFS) with a Queue.
1. Create an empty result list.
2. If the root is null, return the empty list.
3. Add the root node to a Queue.
4. While the queue is not empty:
   - Store the current queue size. This tells us how many nodes belong to the current level.
   - Remove each node of that level from the queue.
   - Add its value to the current level list.
   - Add its left and right children to the queue if they exist.
5. Add the completed level to the result.
6. Continue until every level has been processed.
Java Solution
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> list = new ArrayList<>();

        if (root == null)
            return list;

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            int N = q.size();
            List<Integer> level = new ArrayList<>();

            for (int i = 0; i < N; i++) {
                TreeNode f = q.poll();

                level.add(f.val);

                if (f.left != null) {
                    q.add(f.left);
                }

                if (f.right != null) {
                    q.add(f.right);
                }
            }

            list.add(level);
        }

        return list;
    }
}

Example
Input:
root = [3,9,20,null,null,15,7]

Output:
[[3],[9,20],[15,7]]

Why Does q.size() Matter?
The queue contains nodes from the current level and the next level.
Before processing a level, we store:
int N = q.size();

This tells us exactly how many nodes belong to the current level.
After processing those N nodes, their children are already added to the queue, ready for the next level.
Complexity
Time Complexity: O(n)
Every node is visited exactly once.
Space Complexity: O(n)
The queue can contain multiple nodes at the same level.
What I Learned
- How Breadth-First Search (BFS) works on binary trees.
- How a Queue helps process nodes in the correct order.
- How q.size() can be used to separate one tree level from another.
- The difference between simply traversing a tree and specifically grouping nodes level by level.
Takeaway
Today's problem helped me understand that sometimes the data structure we choose naturally gives us the order we need.
A Queue makes level-by-level traversal feel almost like processing people standing in a line — first come, first served.
Day 66 complete — another concept understood, another step forward. 🚀
