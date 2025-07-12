# Debugging My First Attempt at "Find All Numbers Disappeared in an Array"

## 🧠 Problem Summary

Given an array `nums` of length `n`, where each number is in the range `1` to `n`, some numbers appear once, some twice, and some may be missing. The task is to return a list of all numbers in the range `[1, n]` that **do not appear** in `nums`.

---

## 🧪 My First Attempt

### Code:
```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        freq = {}
        res = []

        for i in range(1, len(nums) + 1):
            freq[i] += freq.get(i, 0) + 1

        for i in range(len(nums)):
            if nums[i] in freq:
                freq.get(i, 0) - 1

        # iterate through freq map and check if freq = 1 then append that to a list res and return it
```

---

## ✅ What I Did Right

- **Understood the Goal:** I correctly identified that the task was to find numbers from `1` to `n` that don’t appear in the list.
- **Chose a Useful Data Structure:** I used a dictionary (`freq`) to track occurrences, which is a solid and common approach.
- **Prepared to Collect Results:** I correctly initialized a result list `res` to store the final answer.

---

## ❌ What I Did Wrong

### 1. Incorrect Frequency Initialization
```python
freq[i] += freq.get(i, 0) + 1
```
- This causes a `KeyError` on the first iteration because `freq[i]` doesn’t exist yet.
- Logically wrong: I was adding frequency to numbers `1..n` before knowing if they exist in `nums`.

✅ **Fix:**
```python
freq[num] = freq.get(num, 0) + 1  # Inside a loop over nums
```

---

### 2. Used Index Instead of Value
```python
freq.get(i, 0) - 1
```
- `i` here is an index (0, 1, 2...), not the actual number from the array.
- Even worse: this line does **nothing** — it just computes a value and discards it.

✅ **Fix:**
```python
num = nums[i]
if num in freq:
    freq[num] -= 1
```

---

### 3. Assumed All Numbers Appear Once
```python
for i in range(1, len(nums) + 1):
    freq[i] += ...
```
- I assumed every number from 1 to n appeared at least once — that defeats the purpose of finding missing numbers.
- I should have built the frequency map **from `nums`**, not from `range(1, n+1)`.

---

### 4. Did Not Implement Final Step
```python
# iterate through freq map and check if freq = 1 then append that to a list res and return it
```
- This logic was incomplete and slightly flawed — if a number is missing, it should be **absent** from the map, not have a frequency of 1.

✅ **Fix:**
```python
for i in range(1, len(nums) + 1):
    if i not in freq:
        res.append(i)
```

---

## ✅ Corrected Version

Here’s a clean version of the fixed code:

```python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        freq = {}
        res = []

        for num in nums:
            freq[num] = freq.get(num, 0) + 1

        for i in range(1, len(nums) + 1):
            if i not in freq:
                res.append(i)

        return res
```

---

## 🧠 Lessons Learned

- Always build frequency maps from **actual data**, not assumptions.
- Be careful with the difference between an index (`i`) and the value at that index (`nums[i]`).
- Operations like `.get()` and `- 1` must actually **update** the data structure.
- Commenting a plan is good — but make sure to **implement it**.
