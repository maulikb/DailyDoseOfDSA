# Week 3: Fast and Slow Pointer Pattern in DSA

## What is the Fast and Slow Pointer Pattern?

The **Fast and Slow Pointer Pattern** (also known as the Tortoise and Hare Algorithm) is a common technique used to solve problems involving cyclic data structures, such as linked lists or arrays. It uses two pointers:
- **Fast Pointer**: Moves two steps at a time.
- **Slow Pointer**: Moves one step at a time.

This pattern is particularly useful for detecting cycles, finding the middle of a linked list, or determining the starting point of a cycle.

---

## How Fast and Slow Pointers Work

The idea is that if there is a cycle in the data structure, the fast pointer will eventually "lap" the slow pointer, meeting it inside the cycle. If there is no cycle, the fast pointer will reach the end of the data structure.

---

## LeetCode Problems and Solutions

### Problem 1: [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

#### Problem Statement:
Given the `head` of a linked list, determine if the linked list has a cycle in it.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week3_fast_slow_pointer.py

class ListNode:
    def __init__(self, value=0, next=None):
        self.value = value
        self.next = next

def has_cycle(head):
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

        if slow == fast:
            return True

    return False

# Example Usage
head = ListNode(3)
head.next = ListNode(2)
head.next.next = ListNode(0)
head.next.next.next = ListNode(-4)
head.next.next.next.next = head.next  # Creates a cycle

print(has_cycle(head))  # Output: True
```

---

### Problem 2: [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

#### Problem Statement:
Given the `head` of a singly linked list, return the middle node of the linked list. If there are two middle nodes, return the second middle node.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week3_fast_slow_pointer.py

def find_middle(head):
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow

# Example Usage
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(3)
head.next.next.next = ListNode(4)
head.next.next.next.next = ListNode(5)

middle = find_middle(head)
print(middle.value)  # Output: 3
```

---

### Problem 3: [Cycle Detection and Starting Point](https://leetcode.com/problems/linked-list-cycle-ii/)

#### Problem Statement:
Given the `head` of a linked list, return the node where the cycle begins. If there is no cycle, return `null`.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week3_fast_slow_pointer.py

def detect_cycle(head):
    slow, fast = head, head

    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

        if slow == fast:
            # Cycle detected, find the start of the cycle
            slow = head
            while slow != fast:
                slow = slow.next
                fast = fast.next
            return slow

    return None

# Example Usage
head = ListNode(3)
head.next = ListNode(2)
head.next.next = ListNode(0)
head.next.next.next = ListNode(-4)
head.next.next.next.next = head.next  # Creates a cycle

cycle_start = detect_cycle(head)
print(cycle_start.value if cycle_start else "No cycle")  # Output: 2
```

---

### Problem 4: [Happy Number](https://leetcode.com/problems/happy-number/)

#### Problem Statement:
Write an algorithm to determine if a number `n` is a happy number. A happy number is defined as a number where repeatedly replacing the number by the sum of the squares of its digits eventually leads to `1`. If it loops endlessly in a cycle, it is not a happy number.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week3_fast_slow_pointer.py

def is_happy(n):
    def get_next(number):
        total_sum = 0
        while number > 0:
            digit = number % 10
            total_sum += digit ** 2
            number //= 10
        return total_sum

    slow, fast = n, get_next(n)

    while fast != 1 and slow != fast:
        slow = get_next(slow)
        fast = get_next(get_next(fast))

    return fast == 1

# Example Usage
n = 19
print(is_happy(n))  # Output: True
```

---

### Problem 5: [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)

#### Problem Statement:
Given the `head` of a singly linked list, return `true` if it is a palindrome.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week3_fast_slow_pointer.py

def is_palindrome(head):
    # Find the middle of the linked list
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    # Reverse the second half of the linked list
    prev = None
    while slow:
        temp = slow.next
        slow.next = prev
        prev = slow
        slow = temp

    # Compare the first and second halves
    left, right = head, prev
    while right:
        if left.value != right.value:
            return False
        left = left.next
        right = right.next

    return True

# Example Usage
head = ListNode(1)
head.next = ListNode(2)
head.next.next = ListNode(2)
head.next.next.next = ListNode(1)

print(is_palindrome(head))  # Output: True
```

---

### Problem 6: [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

#### Problem Statement:
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive, there is exactly one repeated number. Return this repeated number.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week3_fast_slow_pointer.py

def find_duplicate(nums):
    slow, fast = nums[0], nums[0]

    while True:
        slow = nums[slow]
        fast = nums[nums[fast]]
        if slow == fast:
            break

    slow = nums[0]
    while slow != fast:
        slow = nums[slow]
        fast = nums[fast]

    return slow

# Example Usage
nums = [1, 3, 4, 2, 2]
print(find_duplicate(nums))  # Output: 2
```

---

## Summary

The Fast and Slow Pointer Pattern is a powerful technique for solving problems involving cyclic data structures or linked lists. By using two pointers moving at different speeds, you can efficiently detect cycles, find the middle of a list, or solve other related problems. Practice the problems above to master this technique!