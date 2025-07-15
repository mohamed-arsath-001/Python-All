# Unique Paths II – Python Solution

This repository contains a Python implementation to calculate the number of unique paths from the top-left to the bottom-right of a 2D grid, considering obstacles.

> 📎 [Problem Link: Unique Paths II](https://leetcode.com/problems/unique-paths-ii/description/?envType=problem-list-v2&envId=dynamic-programming)

## Problem Description

You are given an `m x n` grid where some cells contain obstacles (denoted by `1`), and the rest are empty (denoted by `0`). You can only move **down** or **right** at any point in time.

Your task is to determine the total number of unique paths from the **top-left corner** to the **bottom-right corner**, avoiding obstacles.

### Rules:
- If a cell has a `1`, it is considered **blocked** and cannot be used.
- If the start or end position is blocked, return `0`.

## Example

**Input:**  
```
Grid = [
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

**Output:**  
`2`

**Explanation:**  
There are 2 possible paths:  
1. Right → Right → Down → Down  
2. Down → Down → Right → Right

## Approach Overview

The algorithm uses **top-down dynamic programming with memoization** to efficiently count all valid paths.

### Key Concepts:
- Use recursion to explore all paths moving right or down.
- Store intermediate results in a `memo` dictionary to avoid redundant calculations.
- Return `0` if:
  - The current cell is outside the grid.
  - The cell is an obstacle.
  - The path leads to an invalid destination.
- Return `1` if the bottom-right corner is reached.

## Python Code

```python
class Solution:
    def uniquePathsWithObstacles(self, Grid: List[List[int]]) -> int:
        m, n = len(Grid), len(Grid[0])
        memo = {}

        # Edge case: if start or end is blocked
        if Grid[0][0] == 1 or Grid[m - 1][n - 1] == 1:
            return 0

        def rec(i, j, m, n, memo):
            if i >= m or j >= n:
                return 0
            if Grid[i][j] == 1:
                return 0
            if i == m - 1 and j == n - 1:
                return 1
            if (i, j) in memo:
                return memo[(i, j)]
            
            memo[(i, j)] = rec(i + 1, j, m, n, memo) + rec(i, j + 1, m, n, memo)
            return memo[(i, j)]

        return rec(0, 0, m, n, memo)
```

### Code Breakdown

1. **Base Conditions**  
   ```python
   if Grid[0][0] == 1 or Grid[m - 1][n - 1] == 1:
       return 0
   ```  
   No valid path if the start or end is blocked.

2. **Recursive Function**  
   ```python
   def rec(i, j, m, n, memo):
   ```  
   Traverses from the current cell `(i, j)` toward the bottom-right cell `(m-1, n-1)`.

3. **Invalid Cell**  
   ```python
   if i >= m or j >= n or Grid[i][j] == 1:
       return 0
   ```  
   Prevents moving out of bounds or into obstacles.

4. **Destination Reached**  
   ```python
   if i == m - 1 and j == n - 1:
       return 1
   ```  
   One valid path has been found.

5. **Memoization**  
   ```python
   if (i, j) in memo:
       return memo[(i, j)]
   ```  
   Returns stored result if this subproblem has already been solved.

## Time and Space Complexity

### Time Complexity
- **O(m × n)** in the worst case, where each cell is visited once and stored in `memo`.

### Space Complexity
- **O(m × n)** for the memoization table.
- **O(m + n)** recursion stack depth in the worst case.

## How to Use

To test this code:

```python
sol = Solution()
grid = [
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
print(sol.uniquePathsWithObstacles(grid))  # Output: 2
```

Make sure to run it in an environment where the `List` type is properly imported:

```python
from typing import List
```

## Performance Metrics
- **Runtime:** 0 ms | Beats 100.00%  
- **Memory:** 18.04 MB | Beats 30.39%
