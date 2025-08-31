# Merge Two Sorted Linked Lists

Here’s my write-up for the `mergeTwoLists` function I implemented. The goal was to merge two sorted linked lists into a single sorted one and return the head of that merged list.

## Problem Definition
I needed to take two sorted linked lists, `list1` and `list2`, and merge them into one sorted list without breaking the order.

## My Thought Process
At first, I tried to merge one list into the other directly, but I kept running into issues with handling the head node and keeping track of the references. It got messy quickly. That’s when I realized using a **dummy node** would simplify everything.

## Final Code
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:

        dummy = ListNode()  # dummy node to make things easier
        curr = dummy        # pointer for building the new list

        # Compare nodes from both lists until one runs out
        while list1 and list2:
            if list1.val < list2.val:
                curr.next = list1
                list1 = list1.next
            else:
                curr.next = list2
                list2 = list2.next
            curr = curr.next

        # If one list still has nodes left, attach it
        if list1:
            curr.next = list1
        elif list2:
            curr.next = list2

        # Return the merged list (skip the dummy node)
        return dummy.next
```

## Why This Works
- The **dummy node** makes it super easy to handle the start of the new list without special cases.
- I just keep comparing the current nodes of `list1` and `list2`, always choosing the smaller one.
- Once one list is empty, I can safely attach the rest of the other list since it’s already sorted.

## Complexity
- **Time Complexity**: \(O(m + n)\), since I go through every node once.
- **Space Complexity**: \(O(1)\), because I only use a couple of pointers (plus the dummy).

## Reflection
Using a dummy node really simplified the logic compared to my first attempt. It let me focus on just linking nodes in order without worrying about the head case.

