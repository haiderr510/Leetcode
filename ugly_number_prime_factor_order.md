
# Why Start Dividing by 2 First When Checking Ugly Numbers?

## Background

An **ugly number** is a positive integer whose **only prime factors** are 2, 3, or 5. To check if a number is ugly, the common approach is to repeatedly divide the number by these prime factors until it no longer divides evenly. If after removing all factors of 2, 3, and 5 the number reduces to 1, it is considered ugly.

---

## Different Orders of Division

You can divide the number by 2, 3, and 5 **in any order**, for example:

- Divide by 2 first, then 3, then 5.
- Divide by 3 first, then 2, then 5.
- Divide by 5 first, then 2, then 3.

All will give the **correct result**.

---

## Code Examples

```python
# Starting with 2 first
for p in [2, 3, 5]:
    while n % p == 0:
        n //= p

# Starting with 3 first
for p in [3, 2, 5]:
    while n % p == 0:
        n //= p

# Starting with 5 first
for p in [5, 2, 3]:
    while n % p == 0:
        n //= p
```

---

## Why Start with 2?

1. **2 is the smallest prime factor**, so it’s natural to remove the smallest factors first.
2. **Many numbers are even**, so dividing by 2 repeatedly quickly reduces the number.
3. After dividing out all 2s, the number becomes odd, which can simplify further checks.
4. Starting with 2 tends to be **slightly more efficient** than starting with 3 or 5, but the difference is usually negligible for small inputs.

---

## Summary

| Starting Prime | Reason                                                   |
|----------------|----------------------------------------------------------|
| 2              | Smallest prime; efficiently removes even factors early   |
| 3 or 5         | Correct but might do slightly more work on some inputs   |

---

## Conclusion

While all orders yield the correct answer, **starting with 2 is a common practice for efficiency and simplicity**. If performance matters on large inputs, it’s good to start with the smallest prime factor to reduce the number faster.

---

Let me know if you want me to explain the math behind prime factors or help with related algorithms!
