---
title: "Grind 75"
description: "Grind 75 questions"
dateString: October 2022
draft: false
weight: 104
cover:
  # image: "blog/machine-learning-visualized/cover.jpeg"
  # # caption: "Photo by Lenin Estrada on Unsplash"
---

## [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)

### My solution

```python
class Solution:
    def containsDuplicate(self, nums: List[int]) -> bool:
        myset = set()
        for i in nums:
            print(i)
            if i in myset:
                return True
            myset.add(i)
        return False
```

Notes:
Had the difficulty easy so did not take me long. Just glad I revised what a set() is in python and why it is useful. Honestly also could have used an array instead of a set.

## [Valid Anagram](https://leetcode.com/problems/valid-anagram/)

### My solution

```python
  sarray = []
        tarray = []
        for i in range(len(s)):
            sarray.append(s[i])
        sarray.sort()
        for i in range(len(t)):
            tarray.append(t[i])
        tarray.sort()
        return sarray == tarray
```

Notes: Accepted. No comment

## [Two Sum](https://leetcode.com/problems/two-sum/)

### My solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            other = target - nums[i]
            for j in range(len(nums)):
                if nums[j] == other and j != i:
                    return [i,j]
        return []
```

Notes: It is accepted but was curious to see optimal solution

### Alternative Solution

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        hashmap = {}
        for i in range(len(nums)):
            other = target - nums[i]
            if other in hashmap:
                return [i, hashmap[other]]
            hashmap[nums[i]] = i
        return []
```

Notes: Was told to use hashmap so that the soluton could a run time of O(n).

## [Group Anagrams](https://leetcode.com/problems/group-anagrams/)

### My Solution (not really)

Unfortunately my solution here did not work after trying. Luckily my brother is a genius and explained this problem to me. Here is his solution.

```python
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        dict = {}
        for i in range(len(strs)):
            x = sorted(strs[i])
            string = ""
            for j in x:
                string += j
            if string not in dict:
                dict[string] = []
            dict[string].append(strs[i])
        answer = []
        for i in dict:
            answer.append(dict[i])
        return answer
```
