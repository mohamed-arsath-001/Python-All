# Unique Binary Search Trees II – Python Solution

This repository contains a Python implementation of the solution to the problem **"Unique Binary Search Trees II"**, which appears as Problem 95 on LeetCode.

> 📎 [LeetCode Problem 95 – Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

## Problem Description

Given an integer `n`, generate all **structurally unique** Binary Search Trees (BSTs) that store values from `1` to `n`.

Each tree must satisfy the binary search tree (BST) properties:
- The left subtree of a node contains only nodes with values **less than** the node's value.
- The right subtree of a node contains only nodes with values **greater than** the node's value.
- Both left and right subtrees must also be valid BSTs.

### Example

**Input:**  
`n = 3`

**Expected Output:**  
Return all structurally unique BSTs that store values from `1` to `3`.

You can visualize the expected output trees using the tree diagrams provided on the [problem page](https://leetcode.com/problems/unique-binary-search-trees-ii/).

## Approach Overview

This problem is solved using **recursive backtracking**. The core idea is to recursively choose each value in a given range as a root and generate all valid left and right subtrees that could attach to that root.

### Steps:
1. Iterate through each number from `left` to `right` as the root.
2. Recursively generate all valid left subtrees from `left` to `root - 1`.
3. Recursively generate all valid right subtrees from `root + 1` to `right`.
4. Combine each pair of left and right subtrees with the current root.
5. Return the list of all generated trees.

## Python Code

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

class Solution:
    def generateTrees(self, n: int) -> List[Optional[TreeNode]]:
        def gen(left, right):
            if left > right:
                return [None]  # Base case: return list with None representing an empty subtree

            res = []
            for va in range(left, right + 1):
                # Recursively generate all left subtrees using numbers less than va
                for leftTree in gen(left, va - 1):
                    # Recursively generate all right subtrees using numbers greater than va
                    for rightTree in gen(va + 1, right):
                        # Create a new tree node with value 'va' as root
                        root = TreeNode(va, leftTree, rightTree)
                        # Add this tree to the result list
                        res.append(root)
            return res

        if n == 0:
            return []
        return gen(1, n)
```

### Code Breakdown

1. **`generateTrees(self, n: int)`**  
   Entry point to the algorithm. Starts recursion from `1` to `n` by calling `gen(1, n)`.

2. **`gen(left, right)`**  
   Recursive helper function that returns all unique BSTs that can be formed from the values in the range `[left, right]`.

3. **Base Case**  
   ```python
   if left > right:
       return [None]
   ```  
   If `left` is greater than `right`, no nodes can be placed in the current subtree. Return a list with `None` to indicate an empty tree.

4. **Main Loop**  
   ```python
   for va in range(left, right + 1):
   ```  
   Try every value in the range as the root node of the current tree.

5. **Recursive Subtree Generation**  
   ```python
   for leftTree in gen(left, va - 1):
       for rightTree in gen(va + 1, right):
   ```  
   Generate all combinations of left and right subtrees for the current root value.

6. **Construct and Collect Trees**  
   ```python
   root = TreeNode(va, leftTree, rightTree)
   res.append(root)
   ```  
   Combine each left and right subtree with the current root and store the result.

7. **Return Results**  
   ```python
   return res
   ```  
   After all combinations are processed, return the list of generated trees.

## Time and Space Complexity Analysis

### Time Complexity
The number of unique BSTs that can be generated with `n` nodes is the **n-th Catalan number**, which is:

\[
C_n = \frac{(2n)!}{n!(n+1)!}
\]

For each of these \( C_n \) unique tree structures, we perform operations proportional to the number of nodes `n` (to construct and store the tree).

**Overall Time Complexity:**  
\[
O(C_n \cdot n)
\]

### Space Complexity
- **Recursion Stack**: At most \( O(n) \) due to the depth of recursive calls.
- **Tree Storage**: We return \( C_n \) trees, each with up to `n` nodes.

**Overall Space Complexity:**  
\[
O(C_n \cdot n)
\]

## Folder Structure

```bash
tree/
├── generate_unique_bsts.py   # Python implementation of the solution
└── README.md                 # Full explanation and documentation (this file)
```

## How to Use

You can run this code using any Python 3 interpreter. Ensure you define the `TreeNode` class (as in LeetCode) if you're testing it locally.

### Example Usage:
```python
sol = Solution()
all_trees = sol.generateTrees(3)
```

You can implement a tree visualizer or serializer to print or view the output trees.