**学习到的知识：**  
**1. 数组添加元素 List.append()**  
**2. 尽量使用题目给定的变量，节省内存消耗**

## Problem:

Given an array nums. We define a running sum of an array as runningSum[i] = sum(nums[0]…nums[i]).

Return the running sum of nums.

**Example 1:**
```
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
Explanation: Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].
```

**Example 2:**
```
Input: nums = [1,1,1,1,1]
Output: [1,2,3,4,5]
Explanation: Running sum is obtained as follows: [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1].
```   

**Example 3:**
```
Input: nums = [3,1,2,10,1]
Output: [3,4,6,16,17]
```
 
**Constraints:**  
* 1 <= nums.length <= 1000
* -10^6 <= nums[i] <= 10^6

## Solution:
**1. 数组添加元素 List.append()**  
* 执行用时：52 ms, 在所有 Python3 提交中击败了26.10%的用户  
* 内存消耗：15.1 MB, 在所有 Python3 提交中击败了38.60%的用户
```python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        result = []
        result.append(nums[0])
        for i in range((len(nums)-1)):
            result.append(result[i] + nums[i+1])
        return result
```  

**2. 尽量使用题目给定的变量，节省内存消耗**

Runtime: 76 ms, faster than 35.19% of Python3 online submissions for Running Sum of 1d Array.

Memory Usage: 13.8 MB, less than 99.95% of Python3 online submissions for Running Sum of 1d Array.

```python
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        for i in range(1,len(nums)):
            nums[i] = nums[i] + nums[i-1]
        return nums
```

