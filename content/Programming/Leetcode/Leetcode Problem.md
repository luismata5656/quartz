---
id: Leetcode Problem
aliases: []
tags: []
---

## Problem 1: Two Sum

Given an array of integers $nums$ and an integer $target$, return indices of the two numbers such that they add up to $target$

Each input has exactly one solution, and you may not use the same element twice

Ok, so obviously you loop through the list, and the most efficient way would be to read each num only once and stop as soon as it finds target...

Mock loop algo

1. add num to next index
2. if sum != target, increase index
3. once the list has been fully looped through, remove num and do the sum with the remaining list

Something I've just realized, the $nums$ list cannot be changed unless the index of the numbers is stored in another way, but any other way is inefficient.

enumerate: (index, elem)
Update, solution is accepted, here are the stats:`
Runtime: 2218ms, 34.38%
Memory: 17.17mb, 63.4%`

```python
def twoSum(nums: [int], target: int):
    for i,num in enumerate(nums):
        for y, num2 in enumerate(nums[i+1:]):
            if(num + num2 == target):
                print(i, y+(i+1))
```
