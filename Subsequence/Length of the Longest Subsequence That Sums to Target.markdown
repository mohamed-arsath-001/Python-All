# Length of the Longest Subsequence That Sums to Target – Python Solution

This repository contains a Python implementation to find the **length of the longest subsequence** in a list of integers that sums up exactly to a given target.

> 📎 [Problem Link: Length of the Longest Subsequence That Sums to Target](https://leetcode.com/problems/length-of-the-longest-subsequence-that-sums-to-target/description/)

## Problem Description

You are given an array of integers `nums` and an integer `target`. Your goal is to return the **maximum length** of a subsequence in `nums` such that the **sum of its elements is equal to `target`**.

If there is no such subsequence, return `-1`.

### Notes:
- A subsequence is a sequence derived by deleting some (or no) elements without changing the order of the remaining elements.
- The same element cannot be used more than once unless it appears multiple times in `nums`.

## Example

**Input:**  
`nums = [1, 2, 3, 4, 5]`  
`target = 9`

**Output:**  
`3`

**Explanation:**  
The longest valid subsequence summing to 9 could be:  
- `[2, 3, 4]`  
- `[1, 3, 5]`  
- `[4, 5]` is also valid but has only length 2  
The longest among them has length 3.

## Approach Overview

This solution uses **top-down dynamic programming with memoization**.

### Strategy:
1. Use recursion to explore all possible subsequences.
2. At each index, you can either:
   - **Skip** the current element.
   - **Take** the current element if it doesn't overshoot the target.
3. Use a memoization dictionary `memo[(i, t)]` to store the result of subproblems.
4. Return the maximum length of a valid subsequence.
5. If no valid subsequence exists, return `-1`.

## Python Code

```python
class Solution:
    def lengthOfLongestSubsequence(self, nums: List[int], target: int) -> int:
        memo = {}

        def max_length(i, t):
            if i >= len(nums) or t < 0:
                return float('-inf')  # Invalid path
            if t == 0:
                return 0  # Found a valid subsequence
            if (i, t) in memo:
                return memo[(i, t)]

            # Option 1: skip the current number
            skip = max_length(i + 1, t)

            # Option 2: take the current number (if within bounds)
            take = max_length(i + 1, t - nums[i])
            if take != float('-inf'):
                take += 1

            memo[(i, t)] = max(skip, take)
            return memo[(i, t)]

        result = max_length(0, target)
        return -1 if result <= 0 else result
```

### Code Breakdown

1. **Base Cases**  
   ```python
   if i >= len(nums) or t < 0:
       return float('-inf')
   if t == 0:
       return 0
   ```  
   If we've exhausted the list or overshot the target, return a negative infinite marker.  
   If we hit the exact target sum, return a length of 0 (base for adding further).

2. **Memoization**  
   ```python
   if (i, t) in memo:
       return memo[(i, t)]
   ```  
   Avoid recomputation for the same index and target sum.

3. **Decision Step**  
   ```python
   skip = max_length(i + 1, t)
   take = max_length(i + 1, t - nums[i])
   if take != float('-inf'):
       take += 1
   ```  
   Try skipping or taking the current number, and calculate the best result.

4. **Final Comparison**  
   ```python
   memo[(i, t)] = max(skip, take)
   ```

## Time and Space Complexity

### Time Complexity
- **O(n × t)**, where:
  - `n` = number of elements in `nums`
  - `t` = target sum
  - Each subproblem is defined by a unique `(index, remaining target)` pair.

### Space Complexity
- **O(n × t)** for memoization.
- **O(n)** recursion depth (at most).

## How to Use

Example usage:

```python
sol = Solution()
print(sol.lengthOfLongestSubsequence([1, 2, 3, 4, 5], 9))  # Output: 3
```

Make sure to run this in a Python 3 environment with the `List` type imported:

```python
from typing import List
```