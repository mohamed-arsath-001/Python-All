# Find the Maximum Length of Valid Subsequence I – Python Solution

This repository contains a Python implementation to find the **maximum length of a valid subsequence** from a list of integers where adjacent elements satisfy a specific parity rule.

> 📎 [Problem Link: Find the Maximum Length of Valid Subsequence I](https://leetcode.com/problems/find-the-maximum-length-of-valid-subsequence-i/?envType=daily-question&envId=2025-07-16)

## Problem Description

You are given a list of integers `nums`. You need to find the **length of the longest valid subsequence** where the **sum of each pair of adjacent elements is either always even or always odd**.

### Definition:
- A valid subsequence is one where **all adjacent elements (after choosing them) have the same parity sum** (either always even or always odd).
- The elements must appear **in order** as in the original array, but **they do not need to be contiguous**.

## Example

**Input:**  
`nums = [3, 2, 5, 6, 1]`

**Output:**  
`3`

**Explanation:**  
One valid subsequence is `[3, 5, 1]` where every adjacent pair (3+5=8, 5+1=6) results in even sums.  
Another example with odd parity would be `[2, 5, 6]` (2+5=7, 5+6=11).

## Approach Overview

This solution uses a greedy linear scan combined with parity checks.

### Strategy:
1. Iterate through the array twice:
   - Once assuming adjacent sums must be **even** (`parity = 0`)
   - Once assuming adjacent sums must be **odd** (`parity = 1`)
2. In each pass:
   - Track the length of the longest subsequence that satisfies the sum parity rule.
   - Update the current sequence only if the parity of the sum matches the expected.
3. Return the **maximum length** found in either case.

## Python Code

```python
class Solution:
    def maximumLength(self, nums: List[int]) -> int:
        if len(nums) < 2:
            return len(nums)

        max_len = 1

        for parity in [0, 1]:
            count = 1
            prev = nums[0]
            for i in range(1, len(nums)):
                if (nums[i] + prev) % 2 == parity:
                    count += 1
                    prev = nums[i]
            max_len = max(max_len, count)

        return max_len
```

### Code Breakdown

1. **Initial Check**  
   ```python
   if len(nums) < 2:
       return len(nums)
   ```  
   If the array has fewer than two elements, the maximum length is the array's length.

2. **Iterate Over Both Parity Conditions**  
   ```python
   for parity in [0, 1]:
   ```  
   Try both conditions: even sums (0) and odd sums (1).

3. **Track Valid Subsequences**  
   ```python
   if (nums[i] + prev) % 2 == parity:
       count += 1
       prev = nums[i]
   ```  
   Continue the current subsequence if the sum with the previous value matches the expected parity.

4. **Final Result**  
   ```python
   max_len = max(max_len, count)
   ```  
   Store the maximum of all valid subsequence lengths encountered.

## Time and Space Complexity

### Time Complexity
- **O(n)**, where `n` is the length of `nums`.
  - The list is traversed twice (once for each parity type).

### Space Complexity
- **O(1)**: Constant space used for counters and state tracking.

## How to Use

Example usage:

```python
sol = Solution()
print(sol.maximumLength([3, 2, 5, 6, 1]))  # Output: 3
```

Make sure to run this in a Python 3 environment with the `List` type imported:

```python
from typing import List
```