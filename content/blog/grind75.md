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

## [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/)
### My initial Solution (does not work)

```python
Top K Frequent Elements
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        #hashMap[number] = Frequency
        dict = {}
        for i in nums:
            if i not in dict:
                dict[i] = 0
            dict[i] += 1
        #How do i sort hashmap based on values hmmm?
```

### Solution after watching neetcode video

```python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        hashMap = {}
        freq = [[] for i in range(len(nums) + 1)]
        for n in nums:
            hashMap[n] = 1 + hashMap.get(n, 0)
        for n, c in hashMap.items():
            freq[c].append(n)
        answer = []
        for i in range(len(freq) - 1, 0, -1):
            for j in freq[i]:
                answer.append(j)
                if len(answer) == k:
                    return answer 
        return []
``` 

### [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
### My Solution

```python
    class Solution:
        def productExceptSelf(self, nums: List[int]) -> List[int]:
            answer = []
            for i in range(len(nums)):
                current = 1
                for j in range(len(nums)):
                    if i != j:
                        current = current * nums[j]
                answer.append(current)
            return answer
```

Notes: Passed 18/22 Test cases. However, time limit exceeded.
### New Solution:
    ```python   
    class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        answer = [1] * len(nums)
        prefix = 1
        for i in range(len(nums)):
            answer[i] = prefix
            prefix *= nums[i]
        postfix = 1
        for i in range(len(nums) - 1, -1, -1):
            answer[i] = postfix
            postfix *= nums[i]
        return answer
    ```
### [Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)
### My Solution/neetcode Solution

```python   
class Codec:
    def encode(self, strs: List[str]) -> str:
        """Encodes a list of strings to a single string.
        """
        encoded = ""
        for i in strs:
            encoded += str(len(i)) + "#" + i
        return encoded
         

    def decode(self, s: str) -> List[str]:
        """Decodes a single string to a list of strings.
        """
        answer = []
        # We use a while loop so we can easily change the pointer to the next position
        i = 0
        while i < len(s):
            j = i
            while s[j] != "#":
                j += 1
            length = int(s[i:j])
            answer.append(s[j+1: j + 1 + length])
            i = j + 1 + length
        return answer


# Your Codec object will be instantiated and called as such:
# codec = Codec()
# codec.decode(codec.encode(strs))
```

       
### [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
### My Solution

```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        maximum = 1
        nums.sort()
        current = 1
        for i in range(len(nums) - 1):
            if nums[i] != nums[i + 1]:
                if (nums[i + 1] - nums[i] == 1):
                    current += 1
                else:
                    maximum = max(current, maximum)
                    current = 1
        return max(current, maximum)
```

### [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
### My Solution

```python
class Solution:
    def isPalindrome(self, s: str) -> bool:

        i, j = 0, len(s) - 1

        while i < j:
            while i < j and not s[i].isalnum():
                i += 1
            while i < j and not s[j].isalnum():
                j -= 1

            if s[i].lower() != s[j].lower():
                return False

            i += 1
            j -= 1

        return True
```