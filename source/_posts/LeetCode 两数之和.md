title: LeetCode 两数之和系列
author: andyhui
tags:
  - algorithms
categories:
  - leetcode
date: 2019-03-05 22:10:00
---
##  [1] [两数之和](https://leetcode-cn.com/problems/two-sum/description/)


### 描述
>  给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
>
> 你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

<!-- more -->
### 示例:

> 给定 nums = [2, 7, 11, 15], target = 9
>
> 因为 nums[0] + nums[1] = 2 + 7 = 9
>  所以返回 [0, 1]

### 思路
> 对于本题，给出的数组是未排序的，若两两求和需要$$O(n^{2})$$, 如果排序后再双指针遍历，则需要$$O(nlogn + n)$$, 考虑到`HashMap`，可以$$O(1)$$ 查找，因此对于一个数字nums[i],如果target-nums[i]出现过，则输出对应位置，若不存在则记录该数字与位置。

###  代码
``` python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if len(nums) < 2:
            return [-1, -1]
        map = {}
        for i in range(len(nums)):
            if target - nums[i] in map:
                return [i, map[target - nums[i]]]
            else:
                map[nums[i]] = i

s = Solution()
print(s.twoSum([2, 7, 11, 15],9))
```
##  [167] [两数之和 II - 输入有序数组](https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/description/)


### 描述
>  给定一个已按照升序排列 的有序数组，找到两个数使得它们相加之和等于目标数。
>
>  函数应该返回这两个下标值 index1 和 index2，其中 index1 必须小于 index2。
>
### 说明:
>
>  返回的下标值（index1 和 index2）不是从零开始的。
>
>  你可以假设每个输入只对应唯一的答案，而且你不可以重复使用相同的元素。

### 示例:

> 输入: numbers = [2, 7, 11, 15], target = 9
>
> 输出: [1,2]
>
> 解释: 2 与 7 之和等于目标数 9 。因此 index1 = 1, index2 = 2 。

### 思路
> 双指针i,j，i指向较小元素，j指向较大元素，
>
> 令 sum = numbers[i]+numbers[j]
>
> 若sum < target,  i+= 1, 使 sum 变大
>
> 若sum > target, j -=  1，使 sum 变小

###  代码
``` python
class Solution(object):
    def twoSum(self, numbers, target):
        """
        :type numbers: List[int]
        :type target: int
        :rtype: List[int]
        """
        i = 0
        j = len(numbers) - 1
        while i < j:
            sum = numbers[i] + numbers[j]
            if sum == target:
                return [i+1, j+1]
            elif sum < target:
                i += 1
            else:
                j -= 1
        return [-1, -1]
            
s = Solution()
print(s.twoSum([2, 7, 11, 15], 9))  
```

##  [653] [两数之和 IV - 输入 BST](https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/description/)

> 剑指Offer34 二叉树中和为某一值的路径

### 描述

>  给定一个二叉搜索树和一个目标结果，如果 BST 中存在两个元素且它们的和等于给定的目标结果，则返回 true。
>
### 示例:

#### 案例 1:

```shell
输入: 
⁠   5
⁠  / \
⁠ 3   6
⁠/ \   \
2   4   7

Target = 9
```

```shell
输出:
True
```

#### 案例 2:

```shell
输入: 
⁠   5
⁠  / \
⁠ 3   6
⁠/ \   \
2   4   7

Target = 28
```

```shell
输出:
False
```

### 思路
> Todo

###  代码
``` python

```

