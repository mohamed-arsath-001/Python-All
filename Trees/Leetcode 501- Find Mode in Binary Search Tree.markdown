# Find Mode in Binary Search Tree – Python Solution

This repository contains a Python implementation to find the mode(s) (i.e., the most frequent element(s)) in a binary search tree (BST).

> 📎 [Problem Link: Find Mode in Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree/)

## Problem Description

Given the `root` of a binary search tree (BST), return all the mode(s) — the value(s) that appear most frequently in the tree.

You may assume the BST has the following properties:
- The left subtree of a node contains only nodes with values **less than or equal to** the node's value.
- The right subtree of a node contains only nodes with values **greater than or equal to** the node's value.
- Duplicate values are allowed in the tree.

### Example

**Input:**  
```
   1
    \
     2
    /
   2
```

**Output:**  
`[2]`

## Approach Overview

The solution involves an **in-order traversal** of the BST to collect all node values in a sorted list. Then, we use a frequency counter to determine which value(s) appear the most.

### Steps:
1. Perform an **in-order traversal** to extract all node values into a list. Since it's a BST, the in-order traversal yields a sorted list of values.
2. Use the `Counter` class from the `collections` module to count the frequency of each value.
3. Identify the **maximum frequency** among all values.
4. Return a list of all values that match this maximum frequency.

## Python Code

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right

from collections import Counter

class Solution(object):
    def findMode(self, root):
        if not root:
            return []

        lst = []

        def tra(node):
            if not node:
                return 
            tra(node.left)
            lst.append(node.val)
            tra(node.right)

        tra(root)

        count = Counter(lst)
        Max = max(count.values())
        mode = [val for val, freq in count.items() if freq == Max]
        return mode
```

### Code Breakdown

1. **In-order Traversal**  
   ```python
   def tra(node):
       if not node:
           return
       tra(node.left)
       lst.append(node.val)
       tra(node.right)
   ```  
   Visits the BST in sorted order and collects values in `lst`.

2. **Count Frequencies**  
   ```python
   count = Counter(lst)
   ```  
   Counts how often each value appears in the list.

3. **Find Maximum Frequency**  
   ```python
   Max = max(count.values())
   ```  
   Finds the highest number of times any value appears.

4. **Extract All Modes**  
   ```python
   mode = [val for val, freq in count.items() if freq == Max]
   ```  
   Filters values that match the maximum frequency.

## Time and Space Complexity

### Time Complexity
- **O(N)**, where `N` is the number of nodes in the tree.
  - In-order traversal takes **O(N)**.
  - Counting and filtering frequencies also take **O(N)**.

### Space Complexity
- **O(N)**:
  - For storing node values (`lst`).
  - For storing frequency counts (`Counter`).
  - For storing the final result (`mode`).

## How to Use

You can run this code in any Python 2 or Python 3 environment. Ensure the `TreeNode` class is properly defined. Example usage:

```python
sol = Solution()
result = sol.findMode(root)  # where 'root' is an instance of TreeNode
print(result)
```

You can manually construct a binary search tree or use a tree-building utility function to test the code.