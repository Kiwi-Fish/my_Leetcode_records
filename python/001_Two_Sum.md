## 知识积累

**1. leetcode上次提交时间记录是20190510，现在已经是20220922了**  
**2. 一些Brute Force可解的方法不到万不得已不要用，时间复杂度O(n2)，会出现Time Limit Exceeded**


## Problem:

1. Two Sum

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

**Example 1:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**
```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```   

**Example 3:**
```
Input: nums = [3,3], target = 6
Output: [0,1]
```
 
**Constraints:**  
*  2 <= nums.length <= 104
* -10^9 <= nums[i] <= 10^9
* -10^9 <= target <= 10^9
* Only one valid answer exists.

**Follow-up:** Can you come up with an algorithm that is less than O(n2) time complexity?

## Solution: Brute Force
**2. 一些Brute Force可解的方法不到万不得已不要用，时间复杂度O(n2)，会出现Time Limit Exceeded**   
The brute force approach is simple. Loop through each element x and find if there is another value that equals to target-X   
Complexity Analysis
* Time complexity : O(n^2)，每一轮循环的时间复杂度是O(n)，故总的时间复杂度是O(n^2)
* Space complexity : O(1)

**Wrong Answer**  
首先尝试On方的解法正不正确，没注意两个坐标不重复
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(len(nums)):
                if nums[i] + nums[j] == target:
                    return [i,j]
```  
```
Input: nums = [3,2,4], target = 6
Output: [0,0]
Expected: [1,2]
```

**Time Limit Exceeded**  
修改上述bug后，O(n2)超出时间
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1,len(nums)):
                if nums[i] + nums[j] == target:
                    return [i,j]
```  
```
Last executed input: [1,2,3,4,5,...] 19999
```
但是换另一种写法就不超出时间
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(len(nums)-i-1):
                if nums[i] + nums[j+i+1] == target:
                    return [i,j+i+1]
```  
Runtime: 8834 ms, faster than 5.00% of Python3 online submissions for Two Sum.
Memory Usage: 15 MB, less than 76.98% of Python3 online submissions for Two Sum.



**2.  **

Runtime: 

Memory Usage: 

```python
class Solution:

```

