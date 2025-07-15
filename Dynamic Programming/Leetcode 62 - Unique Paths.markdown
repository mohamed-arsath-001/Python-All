# Unique Paths – Python Solution

This repository contains a Python implementation to calculate the number of unique paths from the top-left to the bottom-right corner of an `m x n` grid, moving only right or down.

> 📎 [Problem Link: Unique Paths](https://leetcode.com/problems/unique-paths/)

## Problem Description

You are given two integers `m` and `n` representing the number of rows and columns in a grid. You are initially located at the top-left corner `(0, 0)` and you want to reach the bottom-right corner `(m-1, n-1)`.

You can only move:
- **Right**
- **Down**

Your task is to calculate how many unique paths exist to reach the destination.

## Example

**Input:**  
`m = 3, n = 7`

**Output:**  
`28`

## Approach Overview

This solution uses **recursion with memoization (top-down dynamic programming)**.

### Core Idea:
- At each step, you can either go **right** `(i, j+1)` or **down** `(i+1, j)`.
- Use recursion to explore both directions from each cell.
- Store results in a memoization dictionary to avoid recomputing overlapping subproblems.

## Python Code

```python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        memo = {}

        def rec(i, j, m, n, memo):
            if i >= m or j >= n:
                return 0  # Out of bounds
            if i == m - 1 and j == n - 1:
                return 1  # Reached destination
            if (i, j) in memo:
                return memo[(i, j)]  # Return cached result

            # Explore right and down
            memo[(i, j)] = rec(i + 1, j, m, n, memo) + rec(i, j + 1, m, n, memo)
            return memo[(i, j)]

        return rec(0, 0, m, n, memo)
```

### Code Breakdown

1. **Base Cases**  
   ```python
   if i >= m or j >= n:
       return 0
   ```  
   Invalid move outside the grid.

   ```python
   if i == m - 1 and j == n - 1:
       return 1
   ```  
   Valid path reached destination.

2. **Memoization**  
   ```python
   if (i, j) in memo:
       return memo[(i, j)]
   ```  
   Avoid recomputation by storing already-solved subproblems.

3. **Recursive Relation**  
   ```python
   memo[(i, j)] = rec(i + 1, j, m, n, memo) + rec(i, j + 1, m, n, memo)
   ```  
   Total paths from current cell = paths from down + paths from right.

## Time and Space Complexity

### Time Complexity
- **O(m × n)**: Each cell is computed once due to memoization.

### Space Complexity
- **O(m × n)** for memoization dictionary.
- **O(m + n)** for the recursion call stack depth (at most one full path from top-left to bottom-right).

## How to Use

Example usage:

```python
sol = Solution()
print(sol.uniquePaths(3, 7))  # Output: 28
```

Make sure to run this in a Python 3 environment.