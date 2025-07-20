
## Write-up: Fixing My Sliding Window Logic for "Max Consecutive Ones III"

### Problem
Given a binary array `nums` and an integer `k`, the task is to return the maximum number of consecutive `1`s in the array if at most `k` `0`s can be flipped.

---

### Buggy Code

```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        count = 0
        left = 0
        length = 0
        res = 0

        for right in range(1, len(nums)):
            length = right - left + 1
            res = max(length, res)
            if count >= k:
                left += 1
            if nums[left] == 0:
                count += 1
            if nums[right] == 0:
                count += 1
        return res
```

---

### What Went Wrong

1. **Incorrect loop range**  
   The loop starts at index 1 (`range(1, len(nums))`), which skips the first element. This is unnecessary and breaks the logic when the first few elements are important to the valid window.

2. **Updating `res` before validating the window**  
   The result `res` was updated before checking if the number of flipped zeroes exceeded `k`. This could include invalid windows in the result.

3. **Improper condition to shrink the window**  
   The shrinking logic uses `if count >= k:` which is not always correct. We only want to shrink the window while the number of zeroes exceeds `k`, not when it equals it.

4. **Flawed `count` update**  
   The line `if nums[left] == 0: count += 1` is placed after shifting `left`. This means the count is being updated based on the new left position, not the one we just removed. Worse, it’s adding to the count when it should be subtracting.

---

### Correct Code

```python
class Solution:
    def longestOnes(self, nums: List[int], k: int) -> int:
        count = 0
        left = 0
        res = 0

        for right in range(len(nums)):
            if nums[right] == 0:
                count += 1

            while count > k:
                if nums[left] == 0:
                    count -= 1
                left += 1

            res = max(res, right - left + 1)

        return res
```

---

### Fix Summary

- Start the loop at index `0`, not `1`.
- Update the `res` only after ensuring the current window has at most `k` flipped zeroes.
- Use `while count > k:` to shrink the window dynamically, not just when `count == k` or `>= k`.
- When shrinking the window, subtract from `count` if the element leaving the window was a zero.

---

### Example Test Case

```python
nums = [1,1,1,0,0,0,1,1,1,1,0]
k = 2
# Output: 6
```

With the corrected logic, the sliding window can expand and contract properly while keeping track of how many zeroes were flipped, ensuring the longest valid subarray is found.
