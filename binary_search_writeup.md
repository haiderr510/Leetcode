
# 🔍 Binary Search Write-Up – LeetCode 704: Binary Search

## 🧠 Problem Overview

You're given a **sorted** array of integers in **ascending order**, and a `target` value. The task is to return the index of the target if it's in the array, or `-1` if it's not.

## ❓ Why Binary Search?

- The array is **sorted**
- The problem asks for a solution in **O(log n)** time

Whenever you see:
> "sorted array" + "O(log n)" time  
You should immediately think of **Binary Search**.

## 🧪 Example

```python
nums = [-1, 0, 3, 5, 9, 12]
target = 9
```

Expected output: `4` (since `nums[4] == 9`)

## ✅ Binary Search Solution (Python)

```python
from typing import List

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        first = 0
        last = len(nums) - 1

        while first <= last:
            mid = first + (last - first) // 2

            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                first = mid + 1
            else:
                last = mid - 1

        return -1
```

## 🕵️ Explanation

1. **Initialize**:
   - `first` is the left boundary
   - `last` is the right boundary

2. **Loop while** `first <= last`:
   - Calculate the `mid` index
   - If `nums[mid] == target`, return the index
   - If `nums[mid] < target`, move `first` right
   - If `nums[mid] > target`, move `last` left

3. If you exit the loop, the element isn't found, so return `-1`.

## ⏱ Time and Space Complexity

- **Time**: `O(log n)` — Each iteration cuts the search space in half.
- **Space**: `O(1)` — We only use a few extra variables.

## 💡 Key Takeaway

If a problem:
- Involves a **sorted** array or search space
- Mentions **logarithmic** time

👉 It's probably a **binary search** problem!
