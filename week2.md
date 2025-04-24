# Week 2: Two Pointers Pattern in DSA

## What is the Two Pointers Pattern?

The **Two Pointers Pattern** is a common algorithmic technique used to solve problems involving sorted arrays, linked lists, or strings. It involves using two pointers (or indices) to traverse the data structure, often from opposite ends or in a specific direction.

This pattern is particularly useful for problems that require finding pairs, triplets, or subarrays that satisfy certain conditions.

### Key Characteristics:
1. **Opposite Direction**: One pointer starts at the beginning, and the other starts at the end of the array.
2. **Same Direction**: Both pointers move in the same direction, often used for problems like removing duplicates or finding subarrays.

---

## How Two Pointers Optimizes Code Complexity

The Two Pointers Pattern reduces the time complexity of brute-force solutions by avoiding nested loops. Instead of iterating through all possible pairs or combinations, the two pointers approach processes the data in linear time (`O(n)`), making it highly efficient.

---

## LeetCode Problems and Solutions

### Problem 1: [Pair with Target Sum](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

#### Problem Statement:
Given a sorted array of integers `nums` and a target integer `target`, find two numbers such that they add up to `target`. Return the indices of the two numbers.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week2_two_pointers.py

def two_sum(nums, target):
    left, right = 0, len(nums) - 1

    while left < right:
        current_sum = nums[left] + nums[right]

        if current_sum == target:
            return [left, right]
        elif current_sum < target:
            left += 1  # Move the left pointer to the right
        else:
            right -= 1  # Move the right pointer to the left

    return []

# Example Usage
nums = [2, 7, 11, 15]
target = 9
print(two_sum(nums, target))  # Output: [0, 1]
```

---

### Problem 2: [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)

#### Problem Statement:
Given a sorted array `nums`, remove the duplicates in-place such that each element appears only once and return the new length.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week2_two_pointers.py

def remove_duplicates(nums):
    if not nums:
        return 0

    write_index = 1  # Pointer to place the next unique element

    for read_index in range(1, len(nums)):
        if nums[read_index] != nums[read_index - 1]:
            nums[write_index] = nums[read_index]
            write_index += 1

    return write_index

# Example Usage
nums = [1, 1, 2, 3, 3]
length = remove_duplicates(nums)
print(length)  # Output: 3
print(nums[:length])  # Output: [1, 2, 3]
```

---

### Problem 3: [Triplet Sum to Zero](https://leetcode.com/problems/3sum/)

#### Problem Statement:
Given an array of integers `nums`, return all unique triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week2_two_pointers.py

def three_sum(nums):
    nums.sort()
    triplets = []

    for i in range(len(nums)):
        if i > 0 and nums[i] == nums[i - 1]:
            continue  # Skip duplicate elements

        left, right = i + 1, len(nums) - 1

        while left < right:
            current_sum = nums[i] + nums[left] + nums[right]

            if current_sum == 0:
                triplets.append([nums[i], nums[left], nums[right]])
                left += 1
                right -= 1

                # Skip duplicates
                while left < right and nums[left] == nums[left - 1]:
                    left += 1
                while left < right and nums[right] == nums[right + 1]:
                    right -= 1
            elif current_sum < 0:
                left += 1
            else:
                right -= 1

    return triplets

# Example Usage
nums = [-1, 0, 1, 2, -1, -4]
print(three_sum(nums))  # Output: [[-1, -1, 2], [-1, 0, 1]]
```

---

### Problem 4: [Container With Most Water](https://leetcode.com/problems/container-with-most-water/)

#### Problem Statement:
Given an array `height` of non-negative integers, each representing the height of a vertical line, find two lines that together with the x-axis form a container that holds the most water.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week2_two_pointers.py

def max_area(height):
    left, right = 0, len(height) - 1
    max_area = 0

    while left < right:
        current_area = min(height[left], height[right]) * (right - left)
        max_area = max(max_area, current_area)

        if height[left] < height[right]:
            left += 1
        else:
            right -= 1

    return max_area

# Example Usage
height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
print(max_area(height))  # Output: 49
```

---

## Summary

The Two Pointers Pattern is a versatile and efficient approach for solving problems involving arrays or strings. By leveraging two pointers, you can reduce the time complexity of many problems from `O(n^2)` to `O(n)`. Practice the problems above to master this technique!