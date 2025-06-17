# Week 5: Cyclic Sort Pattern in DSA

## What is the Cyclic Sort Pattern?

The **Cyclic Sort Pattern** is an efficient algorithmic technique used to solve problems involving arrays where the numbers are in a specific range (e.g., `1` to `n`). The key idea is to place each number at its correct index in the array by swapping elements.

This pattern is particularly useful for problems that require finding missing numbers, duplicate numbers, or misplaced numbers in an array.

---

## How Cyclic Sort Works

1. Iterate through the array.
2. If the current number is not at its correct index, swap it with the number at its target index.
3. Repeat until all numbers are at their correct indices.

The time complexity of Cyclic Sort is `O(n)` because, in the worst case, each element is swapped at most once.

---

## LeetCode Problems and Solutions

### Problem 1: [Cyclic Sort](https://leetcode.com/problems/sort-an-array/)

#### Problem Statement:
Given an array of integers `nums` where the integers are in the range `[1, n]`, sort the array in-place using Cyclic Sort.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week5_cyclic_sort.py

def cyclic_sort(nums):
    i = 0
    while i < len(nums):
        correct_index = nums[i] - 1
        if nums[i] != nums[correct_index]:
            nums[i], nums[correct_index] = nums[correct_index], nums[i]
        else:
            i += 1
    return nums

# Example Usage
nums = [3, 1, 5, 4, 2]
print(cyclic_sort(nums))  # Output: [1, 2, 3, 4, 5]
```

---

### Problem 2: [Find the Missing Number](https://leetcode.com/problems/missing-number/)

#### Problem Statement:
Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the only number in the range that is missing from the array.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week5_cyclic_sort.py

def find_missing_number(nums):
    i = 0
    while i < len(nums):
        correct_index = nums[i]
        if nums[i] < len(nums) and nums[i] != nums[correct_index]:
            nums[i], nums[correct_index] = nums[correct_index], nums[i]
        else:
            i += 1

    for i in range(len(nums)):
        if nums[i] != i:
            return i

    return len(nums)

# Example Usage
nums = [4, 0, 3, 1]
print(find_missing_number(nums))  # Output: 2
```

---

### Problem 3: [Find All Missing Numbers](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)

#### Problem Statement:
Given an array `nums` of `n` integers where `nums[i]` is in the range `[1, n]`, return all the integers in the range `[1, n]` that do not appear in `nums`.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week5_cyclic_sort.py

def find_disappeared_numbers(nums):
    i = 0
    while i < len(nums):
        correct_index = nums[i] - 1
        if nums[i] != nums[correct_index]:
            nums[i], nums[correct_index] = nums[correct_index], nums[i]
        else:
            i += 1

    missing_numbers = []
    for i in range(len(nums)):
        if nums[i] != i + 1:
            missing_numbers.append(i + 1)

    return missing_numbers

# Example Usage
nums = [4, 3, 2, 7, 8, 2, 3, 1]
print(find_disappeared_numbers(nums))  # Output: [5, 6]
```

---

### Problem 4: [Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/)

#### Problem Statement:
Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]`, return the duplicate number.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week5_cyclic_sort.py

def find_duplicate(nums):
    i = 0
    while i < len(nums):
        correct_index = nums[i] - 1
        if nums[i] != nums[correct_index]:
            nums[i], nums[correct_index] = nums[correct_index], nums[i]
        else:
            i += 1

    for i in range(len(nums)):
        if nums[i] != i + 1:
            return nums[i]

# Example Usage
nums = [3, 1, 3, 4, 2]
print(find_duplicate(nums))  # Output: 3
```

---

### Problem 5: [Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/)

#### Problem Statement:
Given an array of integers `nums` where `nums[i]` is in the range `[1, n]`, return all the integers that appear twice.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week5_cyclic_sort.py

def find_duplicates(nums):
    i = 0
    while i < len(nums):
        correct_index = nums[i] - 1
        if nums[i] != nums[correct_index]:
            nums[i], nums[correct_index] = nums[correct_index], nums[i]
        else:
            i += 1

    duplicates = []
    for i in range(len(nums)):
        if nums[i] != i + 1:
            duplicates.append(nums[i])

    return duplicates

# Example Usage
nums = [4, 3, 2, 7, 8, 2, 3, 1]
print(find_duplicates(nums))  # Output: [2, 3]
```

---

## Summary

The Cyclic Sort Pattern is a powerful technique for solving problems involving arrays with elements in a specific range. By placing each element in its correct position, you can efficiently find missing or duplicate numbers. Practice the problems above to master this technique!