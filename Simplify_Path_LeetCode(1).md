# 🧩 LeetCode Problem: Simplify Path

**Difficulty:** Medium  
**LeetCode Link:** [Simplify Path](https://leetcode.com/problems/simplify-path/)  
**Topic Tags:** Stack, String, Path Simplification, Parsing  
**Language:** Python 3  

---

## 🧠 Problem Summary

Given an **absolute path** for a file (Unix-style), simplify it.  
The resulting path should:
- Start with a single `/`
- Have no extra `/`
- Resolve `.` (current directory) and `..` (parent directory)
- Contain only valid directory names

### Example
```text
Input: "/home/../foo/"
Output: "/foo"
```

```text
Input: "/a/./b/../../c/"
Output: "/c"
```

---

## 💻 Your Draft Code (Initial Attempt)

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        stack = []
        stack.append(path[0])
        count = 2

        for i in range(len(path)):
            if path[i] == "/":
                if not stack or stack[-1] != "/":
                    stack.append(path[i])
            elif path[i].isalpha():
                stack.append(path[i])
            
            if path[i] == "." and stack[-1] == "." and stack[-2] == ".":
                stack.append(path[i])
            if path[i] == "." and stack[-1] == "." and stack[-2] != ".":
                while count > 2:
                    if stack[-1]:
                        stack.pop()
```

### 🔍 Analysis of Attempt
- You understood the **stack-based intent** well — to push directory names and pop when `..` is found.  
- But the code mixed *character-level iteration* with *directory-level logic*, so `".."` couldn’t be detected properly (string tokens are needed).  
- Essentially: You were parsing **by characters** instead of **by segments** (`split('/')`).

---

## ✅ Corrected and Optimal Solution (Python)

```python
class Solution:
    def simplifyPath(self, path: str) -> str:
        stack = []
        parts = path.split('/')

        for part in parts:
            if part == '' or part == '.':
                continue
            elif part == '..':
                if stack:
                    stack.pop()
            else:
                stack.append(part)

        return '/' + '/'.join(stack)
```

---

## 🧩 Step-by-Step Trace

### Example
```text
Input: "/a/./b/../../c/"
```

| Step | `part` | Action | `stack` |
|------|---------|---------|----------|
| 1 | '' | skip | [] |
| 2 | 'a' | push | ['a'] |
| 3 | '.' | skip | ['a'] |
| 4 | 'b' | push | ['a', 'b'] |
| 5 | '..' | pop | ['a'] |
| 6 | '..' | pop | [] |
| 7 | 'c' | push | ['c'] |

**Output:** `"/c"`

---

## ⏱️ Complexity Analysis

| Type | Complexity | Reason |
|------|-------------|--------|
| **Time** | O(n) | We iterate through all path components once |
| **Space** | O(n) | Stack stores simplified directory names |

---

## 🧭 Key Insights
- Always operate on **path components**, not characters.  
- The `stack` mirrors the *real file system traversal*:  
  - Push folder → `cd folder`  
  - Pop folder → `cd ..`  
- `"."` and `""` (empty parts from `//`) are just **no-ops**.  
- Rebuilding the final path is just joining with `'/'`.

---

## 🧪 Test Cases

```python
s = Solution()
print(s.simplifyPath("/home/"))          # "/home"
print(s.simplifyPath("/../"))            # "/"
print(s.simplifyPath("/home//foo/"))     # "/home/foo"
print(s.simplifyPath("/a/./b/../../c/")) # "/c"
print(s.simplifyPath("/a/../../b/../c//.//")) # "/c"
```

---

## 🧩 Pattern Recognition

**Pattern Name:** Stack-Based String Simplification  
**Pattern Family:** “Undo / Backtracking via Stack”  
**Similar Problems:**
- `Valid Parentheses`
- `Min Stack`
- `Backspace String Compare`
- `Decode String`

---

## 🧘 Growth Note

This problem marks your **transition from structural logic to abstract state management.**  
You’ve gone from literal interpretation (character stack) → conceptual modeling (directory stack).  
That’s a leap in *algorithmic maturity.*
