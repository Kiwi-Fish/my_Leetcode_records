## 知识积累

**1. leetcode上次提交时间记录是20190510，现在已经是20220922了**  
**2. 一些Brute Force可解的方法不到万不得已不要用，时间复杂度O(n2)，会出现Time Limit Exceeded**
**3.  python 字典用法，用字典作为缓存，使用字典键值规则简化问题。python新建空字典{}或dict() **   
**4.  leetcode多次提交运行时间有时会不一样**    
**5.  enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。简化for循环但没有加快。**    

**To do: 当列表中有重复元素时，list.index()方法只能返回第一个元素的下标，解决方法见167 **

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
* Time complexity : O(n2)，每一轮循环的时间复杂度是O(n)，故总的时间复杂度是O(n2)
* Space complexity : O(1)

**Wrong Answer**  
首先尝试O(n2)的解法正不正确，没注意两个坐标不重复
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
**Time Limit Exceeded**  
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


## Solution: 
**2.  python in、 List.index()用法**   
思路转换成先相减，再查找差值对应的序号
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            if target - nums[i] in nums:
                j = nums.index(target - nums[i])
                if i != j:
                    return [i,j]
```
Runtime: 2330 ms, faster than 27.63% of Python3 online submissions for Two Sum.  
Memory Usage: 14.9 MB, less than 76.98% of Python3 online submissions for Two Sum.  
**To do:**  
缺点：当列表中有重复元素时，list.index()方法只能返回第一个元素的下标，解决方法见167  
167. Two Sum II - Input array is sorted

**Wrong Answer**  
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        buff_dict = {}
        for i in range(len(nums)):
            buff_dict[target-nums[i]] = i
            if nums[i] in buff_dict:
                return [buff_dict[nums[i]],i]
```
出错，
```
Input: nums = [3,2,4], target = 6
Output: [0,0]
Expected: [1,2]
```
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        buff_dict = {}
        for i in range(len(nums)):
            buff_dict[target-nums[i]] = i
            if (nums[i] in buff_dict) and (buff_dict[nums[i]] !=i):
                return [buff_dict[nums[i]],i]
```
也出错，存在重复元素的情况，这样buff_dict[target-nums[i]] = i会覆盖原来的下标，导致最后没有输出。所以要先进行判断。
```
Input: nums = [3,3], target = 6
Output: []
Expected: [0,1]
```
## Good Solution: 
**3.  python 字典用法，用字典作为缓存，使用字典键值规则简化问题。python新建空字典{}或dict()**    
注意if nums[i] not in buff_dict的逻辑，先把第二个目标数的序号放进字典，后续的元素判断是不是第一个目标数，然后返回两个序号  
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        buff_dict = {}
        for i in range(len(nums)):
            if nums[i] not in buff_dict:
                buff_dict[target-nums[i]] = i
            else:
                return [buff_dict[nums[i]],i]
```
Runtime: 128 ms, faster than 48.40% of Python3 online submissions for Two Sum.   
Memory Usage: 15.4 MB, less than 8.85% of Python3 online submissions for Two Sum.      
**4.  leetcode多次提交运行时间有时会不一样**    
Runtime: 59 ms, faster than 98.01% of Python3 online submissions for Two Sum.  
Memory Usage: 15.4 MB, less than 8.85% of Python3 online submissions for Two Sum.   

## Good Solution: 
**5.  enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。简化for循环但没有加快。**    
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        buff_dict = dict()
        for i,num in enumerate(nums):
            if num not in buff_dict:
                buff_dict[target-num] = i
            else:
                return [buff_dict[num],i]
```
Runtime: 145 ms, faster than 39.40% of Python3 online submissions for Two Sum.  
Memory Usage: 15.4 MB, less than 13.94% of Python3 online submissions for Two Sum.      
没有加快速度
