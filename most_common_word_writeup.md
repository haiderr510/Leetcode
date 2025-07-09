## LeetCode Problem Write-Up: Most Common Word

**Problem:** Most Common Word\
**Difficulty:** Easy\
**Category:** String / Hash Map

---

### Objective

Given a paragraph of text and a list of banned words, return the most frequent word that is **not banned**. The answer should be case-insensitive, and punctuation should be ignored.

---

### Initial Approach

I started by converting the entire paragraph to lowercase and splitting it into words using `.split()`. Then I looped through each word and added it to a dictionary to keep track of frequency, skipping any word that was in the banned list. My logic looked something like this:

```python
freq = {}
words = paragraph.lower().split()
for word in words:
    if word not in banned and word in freq:
        freq[word] += 1
    elif word not in banned and word not in freq:
        freq[word] = 1
```

I then tried to return the most frequent word using this line:

```python
return freq with highest pair
```

Which obviously wasn’t valid syntax, and I wasn’t sure how to get the key with the highest value cleanly.

---

### What Went Wrong

- **Punctuation wasn’t removed** — so `"ball,"` and `"ball"` were counted as different words.
- I used `split()` on the paragraph assuming that would give clean words, but it didn’t account for commas, periods, etc.
- My final return statement was pseudo-code and not valid Python.
- The `if/elif` logic for incrementing the dictionary count was repetitive.

---

### Improvements and Fixes

**1. Text Cleaning:**\
I removed punctuation by manually replacing each character with a space:

```python
for ch in "!?',;.":
    paragraph = paragraph.replace(ch, " ")
```

This worked but wasn’t the cleanest way to handle multiple characters.

**2. Frequency Count Simplified:**\
Instead of checking whether the word exists in the dictionary, I just used `dict.get()`:

```python
freq[word] = freq.get(word, 0) + 1
```

**3. Finding the Most Common Word:**\
Instead of iterating through the dictionary manually to find the max, I used:

```python
return max(freq, key=freq.get)
```

Which directly gives the key with the highest value.

---

### Final Version

After cleaning things up, here's the full working solution:

```python
from typing import List

class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        # Remove punctuation
        for ch in "!?',;.":
            paragraph = paragraph.replace(ch, " ")

        # Lowercase and split into words
        words = paragraph.lower().split()

        # Count frequency of non-banned words
        freq = {}
        for word in words:
            if word not in banned:
                freq[word] = freq.get(word, 0) + 1

        # Return word with the highest frequency
        return max(freq, key=freq.get)
```

Later, I simplified the punctuation cleaning step further using `str.translate()` and `str.maketrans()`:

```python
paragraph = paragraph.translate(str.maketrans("!?',;.", "      ")).lower()
```

This cleaned up the code and made it more efficient.

---

### Takeaways

- Removing punctuation properly is crucial when doing text processing.
- `max(dict, key=dict.get)` is a clean and readable way to find the key with the highest value.
- Python has a lot of helpful built-in functions for cleaning strings — using `translate` and `maketrans` avoids writing multiple `.replace()` calls.
- The first version worked conceptually, but it lacked polish and had a few beginner-level bugs that I was able to clean up through iteration.

