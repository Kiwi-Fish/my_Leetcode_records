## 知识积累

**1. leetcode上次提交时间记录是20190510，现在已经是20220922了**  
**2. **


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

## Solution:
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
修改上述bug后，On方超出时间
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(len(nums)):
                if nums[i] + nums[j] == target:
                    return [i,j]
```  
```
Last executed input: [1,2,3,4,5,...] 19999
```


**2.  **

Runtime: 

Memory Usage: 

```python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        for i in range(1,len(nums)):
            nums[i] = nums[i] + nums[i-1]
        return nums
```

