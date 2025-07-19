# Letter Combinations of a Phone Number – Python Solution

This repository contains a clean Python solution using **backtracking** to generate all possible letter combinations that a given digit string could represent based on the mapping of digits to letters on a traditional telephone keypad.

> 🔗 [Problem Link: Letter Combinations of a Phone Number](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)

## Problem Description

Given a string containing digits from `2` to `9`, return all possible letter combinations that the number could represent.

### Mapping:
Each digit maps to a set of characters as shown on a phone keypad:
- `2` → "abc"
- `3` → "def"
- `4` → "ghi"
- `5` → "jkl"
- `6` → "mno"
- `7` → "pqrs"
- `8` → "tuv"
- `9` → "wxyz"

### Constraints:
- `digits` contains only digits from `2` to `9`.
- The order of output does not matter.

## Example

**Input:**  
```python
digits = "23"
```

**Output:**  
```python
["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

## Approach Overview

We use **backtracking (DFS)** to recursively generate all possible letter combinations.

### Steps:
1. Define a digit-to-letter mapping using a dictionary.
2. Use a helper function `backtrack(index, current_string)`:
   - If the current string’s length equals the input digit string length, add it to the result list.
   - Otherwise, for the current digit, try each possible character and recursively continue.
3. Start recursion from index `0` and an empty string.
4. Return the result list.

## Python Code

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if not digits:
            return []

        digit_let = {
            "2": "abc", "3": "def", "4": "ghi", "5": "jkl",
            "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"
        }

        def backtrack(ind, strs):
            if len(strs) == len(digits):
                res.append(strs)
                return
            for letter in digit_let[digits[ind]]:
                backtrack(ind + 1, strs + letter)

        res = []
        backtrack(0, "")
        return res
```

### Code Breakdown

1. **Base Case Check**  
   ```python
   if not digits:
       return []
   ```  
   Return an empty list if the input string is empty.

2. **Digit-to-Letter Mapping**  
   ```python
   digit_let = {
       "2": "abc", "3": "def", "4": "ghi", "5": "jkl",
       "6": "mno", "7": "pqrs", "8": "tuv", "9": "wxyz"
   }
   ```  
   Defines the mapping of digits to their corresponding letters.

3. **Backtracking Function**  
   ```python
   def backtrack(ind, strs):
       if len(strs) == len(digits):
           res.append(strs)
           return
       for letter in digit_let[digits[ind]]:
           backtrack(ind + 1, strs + letter)
   ```  
   Recursively builds combinations by appending each possible letter and moving to the next digit.

4. **Initialization and Return**  
   ```python
   res = []
   backtrack(0, "")
   return res
   ```  
   Initializes the result list and starts the backtracking process.

## Time and Space Complexity

### Time Complexity
- **O(3ⁿ × 4ᵐ)**, where:
  - `n` is the number of digits mapping to 3 letters (e.g., 2, 3, 4, 5, 6, 8).
  - `m` is the number of digits mapping to 4 letters (e.g., 7, 9).
  - Each digit contributes a factor based on its letter count (3 or 4).

### Space Complexity
- **O(3ⁿ × 4ᵐ)** for storing the result.
- **O(n)** for the recursion stack depth, where `n` is the length of the input string.

## How to Use

Example usage:

```python
sol = Solution()
print(sol.letterCombinations("23"))  # Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]
```

Make sure to run this in a Python 3 environment with the `List` type imported:

```python
from typing import List
```