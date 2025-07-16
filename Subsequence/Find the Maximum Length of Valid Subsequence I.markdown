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

This solution uses a hybrid strategy combining counting and linear scanning with parity checks.

### Strategy:
1. **Count Same Parity Subsequences:**
   - Count the number of even and odd numbers to determine the maximum length of a subsequence where all elements have the same parity (all even or all odd), as adjacent sums will be even in this case.
2. **Track Alternating Parity Subsequences:**
   - Scan the array to find the longest subsequence where adjacent elements alternate in parity (odd-even or even-odd), ensuring odd sums.
3. **Return the Maximum:**
   - Compare the lengths of the same-parity subsequence and alternating-parity subsequence, returning the larger value.

## Python Code

```python
class Solution:
    def maximumLength(self, nums: List[int]) -> int:
        same_even = 0
        same_odd = 0

        for num in nums:
            if num % 2 == 0:
                same_even += 1
            else:
                same_odd += 1

        max_even_parity = max(same_even, same_odd)

        max_alternating = 1
        prev = nums[0] % 2
        count = 1
        for i in range(1, len(nums)):
            if (nums[i] % 2) != prev:
                count += 1
                prev = nums[i] % 2
        max_alternating = max(max_alternating, count)

        return max(max_even_parity, max_alternating)
```

### Code Breakdown

1. **Initial Check and Counting**  
   ```python
   same_even = 0
   same_odd = 0
   for num in nums:
       if num % 2 == 0:
           same_even += 1
       else:
           same_odd += 1
   max_even_parity = max(same_even, same_odd)
   ```  
   Counts the number of even and odd elements to find the maximum length of a subsequence with the same parity (even sums).

2. **Track Alternating Parity**  
   ```python
   max_alternating = 1
   prev = nums[0] % 2
   count = 1
   for i in range(1, len(nums)):
       if (nums[i] % 2) != prev:
           count += 1
           prev = nums[i] % 2
   max_alternating = max(max_alternating, count)
   ```  
   Builds the longest subsequence where adjacent elements alternate in parity (odd sums).

3. **Final Result**  
   ```python
   return max(max_even_parity, max_alternating)
   ```  
   Returns the maximum length between the same-parity and alternating-parity subsequences.

## Time and Space Complexity

### Time Complexity
- **O(n)**, where `n` is the length of `nums`.
  - One pass to count parity, and one pass to check alternating parity.

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