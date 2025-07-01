# Two Sum II – Write-up

## Problem Summary

Given a sorted array `numbers` and a `target` value, return the 1-based indices of the two numbers that add up to the target. The array is guaranteed to have exactly one solution, and the same element cannot be used twice.

## My Solution

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1

        while l < r:
            if numbers[l] + numbers[r] == target:
                return [l + 1, r + 1]
            if numbers[l] + numbers[r] > target:
                r -= 1
            if numbers[l] + numbers[r] < target:
                l += 1
```

## What I Did Right

- Recognized that the input array is sorted, so the two-pointer technique is optimal.
- Initialized one pointer at the beginning (`l`) and one at the end (`r`) of the array.
- Moved the pointers inward based on the comparison of `numbers[l] + numbers[r]` with the `target`.
- Returned the 1-based indices as required by the problem.

## What I Could Improve

- The last two `if` statements can be changed to `elif` and `else` for cleaner control flow, since only one of the conditions will be true on each iteration.
- The sum calculation can be stored in a temporary variable to avoid repeating the same addition multiple times.

## Optimized Version

```python
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1

        while l < r:
            current_sum = numbers[l] + numbers[r]
            if current_sum == target:
                return [l + 1, r + 1]
            elif current_sum > target:
                r -= 1
            else:
                l += 1
```

## Time and Space Complexity

- **Time Complexity:** O(n) — Only one pass through the array using two pointers.
- **Space Complexity:** O(1) — No extra space is used beyond a few variables.
