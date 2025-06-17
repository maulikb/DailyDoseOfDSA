# Week 4: Merge Intervals Pattern in DSA

## What is the Merge Intervals Pattern?

The **Merge Intervals Pattern** is a common algorithmic technique used to solve problems involving overlapping intervals. This pattern is particularly useful when working with problems that require merging, inserting, or finding gaps between intervals.

The key idea is to:
1. **Sort the intervals** based on their start times.
2. **Iterate through the intervals** and merge overlapping intervals by comparing the current interval with the previous one.

---

## How Merge Intervals Optimizes Code Complexity

By sorting the intervals and iterating through them once, the Merge Intervals Pattern reduces the time complexity of brute-force solutions. Sorting takes `O(n log n)`, and iterating through the intervals takes `O(n)`, resulting in an overall time complexity of `O(n log n)`.

---

## LeetCode Problems and Solutions

### Problem 1: [Merge Intervals](https://leetcode.com/problems/merge-intervals/)

#### Problem Statement:
Given an array of intervals where `intervals[i] = [start, end]`, merge all overlapping intervals and return an array of the non-overlapping intervals.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week4_merge_intervals.py

def merge_intervals(intervals):
    intervals.sort(key=lambda x: x[0])  # Sort intervals by start time
    merged = []

    for interval in intervals:
        # If the list is empty or there is no overlap, add the interval
        if not merged or merged[-1][1] < interval[0]:
            merged.append(interval)
        else:
            # Merge the intervals
            merged[-1][1] = max(merged[-1][1], interval[1])

    return merged

# Example Usage
intervals = [[1, 3], [2, 6], [8, 10], [15, 18]]
print(merge_intervals(intervals))  # Output: [[1, 6], [8, 10], [15, 18]]
```

---

### Problem 2: [Insert Interval](https://leetcode.com/problems/insert-interval/)

#### Problem Statement:
Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week4_merge_intervals.py

def insert_interval(intervals, new_interval):
    result = []
    i = 0

    # Add all intervals that come before the new interval
    while i < len(intervals) and intervals[i][1] < new_interval[0]:
        result.append(intervals[i])
        i += 1

    # Merge overlapping intervals
    while i < len(intervals) and intervals[i][0] <= new_interval[1]:
        new_interval[0] = min(new_interval[0], intervals[i][0])
        new_interval[1] = max(new_interval[1], intervals[i][1])
        i += 1
    result.append(new_interval)

    # Add all intervals that come after the new interval
    while i < len(intervals):
        result.append(intervals[i])
        i += 1

    return result

# Example Usage
intervals = [[1, 3], [6, 9]]
new_interval = [2, 5]
print(insert_interval(intervals, new_interval))  # Output: [[1, 5], [6, 9]]
```

---

### Problem 3: [Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/)

#### Problem Statement:
Given two lists of closed intervals, `firstList` and `secondList`, return their intersection.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week4_merge_intervals.py

def interval_intersection(first_list, second_list):
    i, j = 0, 0
    result = []

    while i < len(first_list) and j < len(second_list):
        # Find the intersection between two intervals
        start = max(first_list[i][0], second_list[j][0])
        end = min(first_list[i][1], second_list[j][1])

        if start <= end:
            result.append([start, end])

        # Move the pointer of the interval that ends first
        if first_list[i][1] < second_list[j][1]:
            i += 1
        else:
            j += 1

    return result

# Example Usage
first_list = [[0, 2], [5, 10], [13, 23], [24, 25]]
second_list = [[1, 5], [8, 12], [15, 24], [25, 26]]
print(interval_intersection(first_list, second_list))
# Output: [[1, 2], [5, 5], [8, 10], [15, 23], [24, 24], [25, 25]]
```

---

### Problem 4: [Employee Free Time](https://leetcode.com/problems/employee-free-time/)

#### Problem Statement:
Given a list of employees, where each employee has a list of non-overlapping intervals, return the list of intervals representing the free time shared by all employees.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week4_merge_intervals.py

def employee_free_time(schedule):
    intervals = [interval for employee in schedule for interval in employee]
    intervals.sort(key=lambda x: x[0])

    merged = []
    for interval in intervals:
        if not merged or merged[-1][1] < interval[0]:
            merged.append(interval)
        else:
            merged[-1][1] = max(merged[-1][1], interval[1])

    free_time = []
    for i in range(1, len(merged)):
        free_time.append([merged[i - 1][1], merged[i][0]])

    return free_time

# Example Usage
schedule = [[[1, 2], [5, 6]], [[1, 3]], [[4, 10]]]
print(employee_free_time(schedule))  # Output: [[3, 4]]
```

---

### Problem 5: [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)

#### Problem Statement:
Given an array of meeting time intervals `intervals` where `intervals[i] = [start, end]`, return the minimum number of conference rooms required.

#### Solution:
```python
# filepath: /Users/maulik/Maulik/DailyDataStructreProblems/week4_merge_intervals.py

import heapq

def min_meeting_rooms(intervals):
    if not intervals:
        return 0

    intervals.sort(key=lambda x: x[0])
    heap = []  # Min-heap to track end times of meetings

    for interval in intervals:
        # If the room due to free up the earliest is free, reuse it
        if heap and heap[0] <= interval[0]:
            heapq.heappop(heap)

        # Allocate a new room
        heapq.heappush(heap, interval[1])

    return len(heap)

# Example Usage
intervals = [[0, 30], [5, 10], [15, 20]]
print(min_meeting_rooms(intervals))  # Output: 2
```

---

## Summary

The Merge Intervals Pattern is a powerful technique for solving problems involving overlapping intervals. By sorting and merging intervals, you can efficiently solve problems related to scheduling, intersections, and gaps. Practice the problems above to master this technique!