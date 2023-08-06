---
title: "First Day Top Interview 150"
date: 2023-07-14T14:54:23-03:00
tags: ["leetcode", "python"]
---

## Contents

- [Exercise Description](#exercise-description)
- [Code With Me](#code-with-me)
- [Exercise Setup](#exercise-setup)
- [Solution 1](#solution-1)
- [Solution 2](#solution-2)
- [Solution 3](#solution-3)

Today is the first day of my journey with my friend Dennis Dang on doing 
the [Top 150 Interview](https://leetcode.com/studyplan/top-interview-150) 
Study Plan from [Leet Code](https://leetcode.com/)

## Exercise Description

The first exercise is about [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/).
The description is:


    You are given two integer arrays nums1 and nums2, sorted in non-decreasing order,
    and two integers m and n, representing the number of elements in nums1 and nums2
    respectively.

    Merge nums1 and nums2 into a single array sorted in non-decreasing order.

    The final sorted array should not be returned by the function, but instead be 
    stored inside the array nums1. To accommodate this, nums1 has a length of m + n,
    where the first m elements denote the elements that should be merged, and the last
    n elements are set to 0 and should be ignored. nums2 has a length of n.

And also gave us a general example:
    
    Input: nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
    Output: [1,2,2,3,5,6]
    Explanation: The arrays we are merging are [1,2,3] and [2,5,6].
    The result of the merge is [1,2,2,3,5,6] with the underlined elements coming 
    from nums1.

## Code With Me

If you wanna follow my submissions in code, you can check at this [github repo](https://github.com/EduardoBorsa/leetcode)

## Exercise Setup

So then I started my approach in python:

```shell
# terminal command
cd python
source env/bin/activate
touch easy/test_merged_sorted_array.py
nvim easy/test_merged_sorted_array.py
```
Then a base setup for the exercise:

```python
from typing import List

class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> List[int]:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        return nums1

def test_merge_sorted_array():
    solution = Solution()
    assert solution.merge([1, 2, 3, 0, 0, 0], 3, [2, 5, 6], 3) == [1, 2, 2, 3, 5, 6]
    assert solution.merge([1], 1, [], 0) == [1]
    assert solution.merge([0], 0, [1], 1) == [1]
```

## Run Our First Test

Then we got our first failing test:
```python
test_merged_sorted_array.py F                                                                                 

============================================================================ FAILURES ========================
____________________________________________________________________ test_merge_sorted_array _________________

    def test_merge_sorted_array():
        solution = Solution()
>       assert solution.merge([1, 2, 3, 0, 0, 0], 3, [2, 5, 6], 3) == [1, 2, 2, 3, 5, 6]
E       assert [1, 2, 3, 0, 0, 0] == [1, 2, 2, 3, 5, 6]
E         At index 2 diff: 3 != 2
E         Use -v to get more diff

test_merged_sorted_array.py:46: AssertionError
==================================================================== short test summary info =================
FAILED test_merged_sorted_array.py::test_merge_sorted_array - assert [1, 2, 3, 0, 0, 0] == [1, 2, 2, 3, 5, 6]
======================================================================= 1 failed in 0.01s ====================
```

## Solution 1

```python
# Time Complexity O((n + m)log(n + m)) ~> We had to traverse both arrays and the best sort algorithm should take xlog(x)
# Space complexity O(m) ~> We had to copy nums1
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> List[int]:
        # def merge(self, nums1, m, nums2, n) -> None:
        for i in range(n):
            nums1[i + m] = nums2[i]
        nums1.sort()
        return nums1
```

## Solution 2

```python
# Time Complexity O(n+m) ~> We had to traverse both arrays
# Space complexity O(m) ~> We had to copy nums1
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> List[int]:
        p1 = 0
        p2 = 0
        nums1_copy = nums1[:m]

        for p in range(n + m):
            if p2 >= n or (p1 < m and nums1_copy[p1] <= nums2[p2]):
                nums1[p] = nums1_copy[p1]
                p1 += 1
            else:
                nums1[p] = nums2[p2]
                p2 += 1

        return nums1
```

## Solution 3

{{< video src="final_best_solution" >}}

```python
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> List[int]:
        p1 = m - 1
        p2 = n - 1

        for p in range(n + m - 1, -1, -1):
            if p2 < 0:
                break
            if p1 >= 0 and nums1[p1] > nums2[p2]:
                nums1[p] = nums1[p1]
                p1 -= 1
            else:
                nums1[p] = nums2[p2]
                p2 -= 1

        return nums1
```

Thank you for reading

