# Week 1: Sliding Window Pattern in DSA

## What is the Sliding Window Pattern?

The **Sliding Window Pattern** is a commonly used technique in data structures and algorithms to solve problems involving arrays or lists. It is particularly useful when dealing with problems that require finding subarrays or substrings that meet certain conditions.

The idea is to use a "window" (a subset of the array or string) that slides over the data structure. Instead of recalculating the result for overlapping parts of the window, we reuse the previous computation, which helps optimize the solution.

### Key Characteristics:
1. **Fixed-size Window**: The window size remains constant throughout the traversal.
2. **Dynamic-size Window**: The window size changes dynamically based on the problem's constraints.

---

## How Sliding Window Optimizes Code Complexity

The sliding window technique reduces the time complexity of brute-force solutions by avoiding redundant calculations. Instead of iterating through all possible subarrays or substrings, the sliding window approach processes the data in linear time (`O(n)`), making it highly efficient.

### Example: Brute Force vs Sliding Window

#### Problem: Find the maximum sum of a subarray of size `k`.

**Brute Force Approach**:
- Iterate through all possible subarrays of size `k`.
- Calculate the sum for each subarray.
- Time Complexity: `O(n * k)`.

**Sliding Window Approach**:
- Use a single loop to maintain a running sum of the current window.
- Add the next element and remove the first element of the window as it slides.
- Time Complexity: `O(n)`.

---

## LeetCode Problems and Solutions

### Problem 1: [Maximum Sum of a Subarray of Size K](https://leetcode.com/problems/maximum-average-subarray-i/)

#### Problem Statement:
Given an array of integers `nums` and an integer `k`, find the maximum sum of a subarray of size `k`.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week1_sliding_window.py

def max_sum_subarray(nums, k):
    max_sum = float('-inf')
    window_sum = 0
    start = 0

    for end in range(len(nums)):
        window_sum += nums[end]  # Add the next element to the window

        # Check if the window size is reached
        if end >= k - 1:
            max_sum = max(max_sum, window_sum)  # Update the maximum sum
            window_sum -= nums[start]  # Remove the first element of the window
            start += 1  # Slide the window forward

    return max_sum

# Example Usage
nums = [2, 1, 5, 1, 3, 2]
k = 3
print(max_sum_subarray(nums, k))  # Output: 9
```

---

### Problem 2: [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

#### Problem Statement:
Given a string `s`, find the length of the longest substring without repeating characters.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week1_sliding_window.py

def length_of_longest_substring(s):
    char_set = set()
    max_length = 0
    start = 0

    for end in range(len(s)):
        while s[end] in char_set:
            char_set.remove(s[start])  # Remove the leftmost character
            start += 1  # Slide the window forward
        char_set.add(s[end])  # Add the current character to the set
        max_length = max(max_length, end - start + 1)

    return max_length

# Example Usage
s = "abcabcbb"
print(length_of_longest_substring(s))  # Output: 3
```

---

### Problem 3: [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

#### Problem Statement:
Given an array of positive integers `nums` and a positive integer `target`, find the minimal length of a contiguous subarray of which the sum is greater than or equal to `target`. If there is no such subarray, return `0`.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week1_sliding_window.py

def min_subarray_len(target, nums):
    min_length = float('inf')
    window_sum = 0
    start = 0

    for end in range(len(nums)):
        window_sum += nums[end]  # Add the next element to the window

        while window_sum >= target:
            min_length = min(min_length, end - start + 1)  # Update the minimum length
            window_sum -= nums[start]  # Remove the first element of the window
            start += 1  # Slide the window forward

    return min_length if min_length != float('inf') else 0

# Example Usage
nums = [2, 3, 1, 2, 4, 3]
target = 7
print(min_subarray_len(target, nums))  # Output: 2
```

---

### Problem 4: [Permutation in String](https://leetcode.com/problems/permutation-in-string/)

#### Problem Statement:
Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week1_sliding_window.py

from collections import Counter

def check_inclusion(s1, s2):
    s1_count = Counter(s1)
    window_count = Counter()
    start = 0

    for end in range(len(s2)):
        window_count[s2[end]] += 1

        # If the window size exceeds the size of s1, shrink it
        if end - start + 1 > len(s1):
            if window_count[s2[start]] == 1:
                del window_count[s2[start]]
            else:
                window_count[s2[start]] -= 1
            start += 1

        # Check if the current window matches the frequency of s1
        if window_count == s1_count:
            return True

    return False

# Example Usage
s1 = "ab"
s2 = "eidbaooo"
print(check_inclusion(s1, s2))  # Output: True
```

---

### Problem 5: [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/)

#### Problem Statement:
You are given an array of integers `nums`, and there is a sliding window of size `k` that moves from the left to the right. Return the maximum value in each window.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week1_sliding_window.py

from collections import deque

def max_sliding_window(nums, k):
    result = []
    dq = deque()  # Store indices of elements in the current window

    for i in range(len(nums)):
        # Remove indices that are out of the current window
        if dq and dq[0] < i - k + 1:
            dq.popleft()

        # Remove indices of smaller elements as they are not useful
        while dq and nums[dq[-1]] < nums[i]:
            dq.pop()

        dq.append(i)

        # Add the maximum element of the current window to the result
        if i >= k - 1:
            result.append(nums[dq[0]])

    return result

# Example Usage
nums = [1, 3, -1, -3, 5, 3, 6, 7]
k = 3
print(max_sliding_window(nums, k))  # Output: [3, 3, 5, 5, 6, 7]
```

---

## Summary

The sliding window pattern is a powerful tool for solving problems efficiently. By maintaining a subset of the data and reusing computations, it significantly reduces time complexity compared to brute-force approaches. Practice the problems above to master this technique!