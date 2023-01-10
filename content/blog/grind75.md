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

## [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
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
## [Encode and Decode Strings](https://leetcode.com/problems/encode-and-decode-strings/)
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

       
## [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/)
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

## [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)
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

## [3Sum](https://leetcode.com/problems/3sum/)
### My Solution

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        answer = []
        nums.sort()
        for i, a in enumerate(nums):
            if i > 0 and a == nums[i - 1]:
                continue
            l = i +1
            r = len(nums) - 1
            while l < r:
                threeSum = a + nums[l] + nums[r]
                if threeSum > 0:
                    r -= 1
                elif threeSum < 0:
                    l +=1
                else:
                    answer.append([a, nums[l], nums[r]])
                    l += 1
                    while (nums[l] == nums[l - 1]):
                        l += 1
        return answer
                    
``` 

Notes: It is important to sort the array so traversing the rest of the array will be easier. Also, it is important to check if the current number is the same as the previous number. If it is, then we can skip it because we already checked it. The rest of the implementation is similar to 2Sum.

## [Containter with most water](https://leetcode.com/problems/container-with-most-water/)
### My Solution

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        rightpointer = len(height) - 1
        rightwidth = len(height)
        leftpointer = 0
        leftwidth = 1
        answer = 0
        while leftpointer < len(height):
            while leftpointer < rightpointer:
                length = min(height[leftpointer],height[rightpointer])
                width = rightwidth - leftwidth
                area = length * width
                answer = max(area, answer)
                rightpointer -= 1
                rightwidth -= 1
            leftpointer += 1
            leftwidth += 1
            rightpointer = len(height) - 1
            rightwidth = rightpointer + 1
        return answer
```

Notes: This is a brute force solution. It is not the most efficient solution. However, it is a good starting point. The idea is to have two pointers, one at the beginning and one at the end. Then, we calculate the area of the container. Then, we move the pointer with the smaller height. This is because if we move the pointer with the larger height, the area will always be smaller. We keep doing this until the two pointers meet.

### Revised Solution after watching neetcode video

```python 
class Solution:
    def maxArea(self, height: List[int]) -> int:
        left = 0
        right = len(height) - 1
        answer = 0
        while left < right:
            leftpos = left + 1
            rightpos = right + 1
            length = rightpos - leftpos
            width = min(height[left], height[right])
            area = width * length
            answer = max(area, answer)
            
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
        return answer
```
In here we will still be using 2 pointers. However instead of calculating every area possible, we will only calculate the area of the container that is formed by the two pointers. Then, we will move the pointer with the smaller height. This is because if we move the pointer with the larger height, the area will always be smaller. We keep doing this until the two pointers meet.

## [Best time to buy and sell stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

### My Solution

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        left = 0
        right = len(prices) - 1
        answer = 0
        while left < len(prices):
            while left < right:
                current = prices[right] - prices[left]
                if current > answer:
                    answer = current
                right -= 1
            left += 1
            right = len(prices) - 1
        return answer
```

Notes: This is a brute force solution. It is not the most efficient solution. However, it is a good starting point. The idea is to have two pointers, one at the beginning and one at the end. Then, we calculate the difference between the two prices. Then, we move the pointer with the smaller price. This is because if we move the pointer with the larger price, the difference will always be smaller. We keep doing this until the two pointers meet.

### Revised Solution after watching neetcode video

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        l = 0
        r = 1
        answer = 0
        while r < len(prices):
            if prices[r] - prices[l] > 0:
                profit = prices[r] - prices[l]
                answer = max(profit, answer)
            else:
                l = r
            r += 1
        return answer
```

Notes: In here we will still be using 2 pointers. However instead of calculating every difference possible, we will only calculate the difference of the two pointers. Then, we will move the pointer with the smaller price. This is because if we move the pointer with the larger price, the difference will always be smaller. We keep doing this until the two pointers meet.

## [Longest Substring without repeating characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

### My Solution

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        charSet = set()
        l = 0
        res = 0

        for r in range(len(s)):
            while s[r] in charSet:
                charSet.remove(s[l])
                l += 1
            charSet.add(s[r])
            res = max(res, r- l + 1)
        return res
```
Notes: This is a sliding window problem. The idea is to have two pointers, one at the beginning and one at the end. Then, we move the right pointer until we find a repeating character. Then, we move the left pointer until we find a non-repeating character. We keep doing this until the right pointer reaches the end of the string.

## [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/)
### My Solution (watched neetcode already)

```python
class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        l = 0 
        hashMap = {}
        res = 0 
        
        for r in range(len(s)):
            hashMap[s[r]] = hashMap.get(s[r], 0) + 1

            while (r - l + 1) - max(hashMap.values()) > k:
                hashMap[s[l]] -= 1
                l += 1

            res = max(res, r - l + 1)
        return res
```
Notes: This is a sliding window problem. The idea is to have two pointers, one at the beginning and one at the end. Then, we move the right pointer until we find a repeating character. Then, we move the left pointer until we find a non-repeating character. We keep doing this until the right pointer reaches the end of the string.

## [Valid Paranthesis](https://leetcode.com/problems/valid-parentheses/)
### My Solution

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        matcher = {")": "(", "}" : "{", "]" : "["}
        for c in s:
            if c in matcher:
                if stack and stack[-1] == matcher[c]:
                    stack.pop()
                else:
                    return False
            else:
                stack.append(c)
        return True if not stack else False
```
Notes: This is a stack problem. The idea is to have a stack. Then, we iterate through the string. If the character is an opening bracket, we push it into the stack. If the character is a closing bracket, we check if the top of the stack is the corresponding opening bracket. If it is, we pop the top of the stack. If it is not, we return False. If we reach the end of the string, we check if the stack is empty. If it is, we return True. If it is not, we return False.

## [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/)

### My Solution

```python
    class Solution:
    def findMin(self, nums: List[int]) -> int:
        return min(nums)
```

I initially laughed because this solution worked. But here is the actual solution with binary search.

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        res = nums[0]
        l = 0
        r = len(nums) - 1
        while l <= r:
            if nums[l] < nums[r]:
                return min(res, nums[l])
            mid = (l + r) // 2 
            res = min(res, nums[mid])
            if nums[mid] >= nums[l]:
                l = mid + 1
            else:
                r = mid - 1
        return res
```

Notes: This is a binary search problem. The idea is to have two pointers, one at the beginning and one at the end. Then, we calculate the middle of the two pointers. If the middle is greater than the left pointer, we move the left pointer to the middle. If the middle is less than the right pointer, we move the right pointer to the middle. We keep doing this until the two pointers meet. Then, we return the minimum of the two pointers.

## [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)

### My Solution

```python
class Solution:
    def findMin(self, nums: List[int]) -> int:
        res = nums[0]
        l = 0
        r = len(nums) - 1
        while l <= r:
            if nums[l] < nums[r]:
                return min(res, nums[l])
            mid = (l + r) // 2 
            res = min(res, nums[mid])
            if nums[mid] >= nums[l]:
                l = mid + 1
            else:
                r = mid - 1
        return res
```

I have already done this problem before so I somehow already knew how to do it. But the idea is to have two pointers, one at the beginning and one at the end. Then, we calculate the middle of the two pointers. If the middle is greater than the left pointer, we move the left pointer to the middle. If the middle is less than the right pointer, we move the right pointer to the middle. We keep doing this until the two pointers meet. Then, we return the minimum of the two pointers.

## [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/submissions/)
### My Solution

```python
class Solution:
    # Definition for singly-linked list.
    # class ListNode:
    #     def __init__(self, val=0, next=None):
    #         self.val = val
    #         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        #Jiro's Solution
        prev = None
        curr = head
        while curr:
            next_temp = curr.next
            curr.next = prev
            prev = curr
            curr = next_temp
            
        return prev
```

Notes: Draw it out in order to understand it more